# Habitat Lab

## Agent
```plantuml
package agent {
    abstract class Agent {
        {abstract} +reset()
        {abstract} +act()
    }
}
```

## Dataset

```plantuml
package dataset {
    class Episode {
        +episode_id: str
        +scene_id: str
        +start_position: List
        +start_rotation: List
        +info: Dict
        -_shortest_path_cache
    }

    class Dataset<EpisodeType> {
        +episodes: List
        {static} scene_from_scene_path()
        {static} get_scenes_to_load()
    }

    Dataset "1" *-- "*" Episode
}
```

## Environment
Environment contains three major components
* Dataset
* Simulator
    - Determine one sort of observation_spaces (sensor_suite)
* Task
    - Determine another sort of observation_spaces (sensor_suite)
    - Determine action_space

```plantuml
package env {
    class Env {
        +observation_space: SpaceDict
        +action_space: SpaceDict
        +number_of_episodes: int
        +sim: Simulator
        +task: EmbodiedTask
        +current_episode: Episode
        +episode_iterator
        +episodes: List
        +episode_start_time: float
        +episode_over: bool
        -_config: Config
        -_dataset: Dataset
        -_current_episode_index: int
        -_max_episode_seconds: int
        -_max_episode_steps: int
        -_elapsed_steps: int
        -_elapsed_seconds: float

        +reset()
        +step()
        +get_metrics()
        -_past_limit()
        -_reset_stats()
        -_update_step_stats()
    }

    class RLEnv {
        -_env: Env
        +habitat_env
        +episodes
        +current_episode
        +observation_space
        +action_space
        +number_of_episodes
        +reward_range
        +reset()
        +step()
        {abstract} +get_reward_range()
        {abstract} +get_reward()
        {abstract} +get_done()
        {abstract} +get_info()
        +seed()
        +render()
        +close()
        +__enter__()
        +__exit__()
    }

    gym.Env <|-- RLEnv
}
```

## Simulator
```plantuml
package simulator {
    abstract class Simulator {
        {abstract} +sensor_suite: SensorSuite
        {abstract} +action_space: Space

        {abstract} +reset(): Observations
        {abstract} +step(): Observations
        {abstract} +seed()
        {abstract} +reconfigure()
        {abstract} +geodesic_distance(): float
        {abstract} +get_agent_state(): AgentState
        {abstract} +get_observation_at(): Observations
        {abstract} +sample_navigable_point(): List[float]
        {abstract} +is_navigable(): bool
        {abstract} +action_space_shortest_path(): List[ShortestPathPoint]
        {abstract} +get_straight_shortest_path_points(): List[List[float]]
        {abstract} +up_vector(): ndarray
        {abstract} +forward_vector(): ndarray
        {abstract} +render()
        +close()
        {abstract} +previous_step_collided(): bool
        +__enter__(): Simulator
        +__exit__()
    }

    class AgentState {
        +position: ndarray
        +rotation: ndarray
    }

    class ShortestPathPoint {
        +position: List
        +rotation: List
        +action: int
    }

    class SensorSuite {
        +sensors: Dict
        +observation_spaces: spaces
        +get(): Sensor
        +get_observations(): Observations
    }

    enum SensorType {
        NULL
        COLOR
        DEPTH
        NORMAL
        SEMANTIC
        PATH
        POSITION
        FORCE
        TENSOR
        TEXT
        MEASUREMENT
        HEADING
        TACTILE
        TOKEN_IDS
    }
}
```

## Embodied Task
* Each `Action` has its own state for each episode, which will be reset in `Action::reset`
* `EmbodiedTask::reset` will reset `_sim` and `actions` state
* `Measure` is used for performance metrics and rewards
    - `reset_metric()` is called from `env.Env` on reset
    - `update_metric()` is called from `env.Env` on step
* `Measurements` is a collection of `Measure`
    - `reset_measures()` call all `measure.reset_metric()`
    - `update_measures()` call all `measure.update_metric()`
    - one measure can depend on other measures, use `check_measure_dependencies()` for assertion

```plantuml
package embodied_task {
    abstract class Action {
        {abstract} +reset()
        {abstract} +step(): Observations
        {abstract} +action_space
    }

    abstract class SimulatorTaskAction {
        -_config: Config
        -_sim: Simulator
    }

    Action <|-- SimulatorTaskAction

    abstract class Measure {
        {abstract} +reset_metric()
        {abstract} +update_metric()
        +get_metric()
        {abstract} +uuid: str
        -_metric
    }

    class Metrics {
        dict
    }

    class Measurements {
        +reset_measures()
        +update_measures()
        +get_metrics() : Metrics
        +check_measure_dependencies()
        -_get_measure_index()
        +measures: Dict
    }

    Measurements "1" *-- "*" Measure
    Measurements::get_metrics -> Metrics

    class EmbodiedTask {
        +measurements: Measurements
        +sensor_suite: SensorSuite
        +actions: OrderedDict
        -_sim: Simulator
        -_dataset: Dataset
        +action_space: ActionSpace
        +is_episode_active: bool
        +reset(): Observations
        +step(): Observations
        +get_action_name()
        {abstract} +overwrite_sim_config(): Config
        {abstract} -_check_episode_is_active(): bool
        +seed()
        -_init_entities()
    }
}

package nav {
    class NavigationGoal {
        +position: List
        +radius
    }

    class RoomGoal {
        +room_id: str
        +room_name: [str]
    }

    NavigationGoal <|-- RoomGoal
    dataset::Episode <|-- NavigationEpisode
    NavigationEpisode "1" *-- "*" NavigationGoal

    class NavigationEpisode {
        +goals: List
        +start_room: [str]
        +shortest_paths
    }

    class Success {
        -_get_uuid(): str
        +reset_metric()
        +update_metric()
    }

    class SPL {
        -_get_uuid(): str
        +reset_metric()
        -_euclidean_distance()
        +update_metric()
    }

    class SoftSPL {
        -_get_uuid(): str
        +reset_metric()
        +update_metric()
    }

    class Collisions {
        -_get_uuid(): str
        +reset_metric()
        +update_metric()
    }

    class DistanceToGoal {
        -_get_uuid(): str
        +reset_metric()
        +update_metric()
    }

    class TopDownMap {
        -_get_uuid(): str
        +get_original_map()
        -_draw_point()
        -_draw_goals_view_points()
        -_draw_goals_positions()
        -_draw_goals_aabb()
        -_draw_shortest_path()
        -_is_on_same_floor()
        +reset_metric()
        +update_metric()
        +get_polar_angle()
        +update_map()
        +update_fog_of_war_mask()
    }

    Measure <|-- Success
    Measure <|-- SPL
    SPL <|-- SoftSPL
    Measure <|-- Collisions
    Measure <|-- DistanceToGoal
    Measure <|-- TopDownMap

    class MoveForwardAction {
        +step()
    }
    class TurnLeftAction {
        +step()
    }
    class TurnRightAction {
        +step()
    }
    class StopAction {
        +reset()
        +step()
    }
    class LookUpAction {
        +step()
    }
    class LookDownAction {
        +step()
    }
    class TeleportAction {
        +step()
        +action_space()
        -_get_uuid()
    }

    SimulatorTaskAction <|-- MoveForwardAction
    SimulatorTaskAction <|-- TurnLeftAction
    SimulatorTaskAction <|-- TurnRightAction
    SimulatorTaskAction <|-- StopAction
    SimulatorTaskAction <|-- LookUpAction
    SimulatorTaskAction <|-- LookDownAction

    class PointGoalSensor {
        -_sim
        -_goal_format
        -_dimensionality
        +get_observation()
    }

    class ImageGoalSensor {
        -_sim
        +get_observation()
    }

    class IntegratedPointGoalGPSAndCompassSensor {
        +get_observation()
    }

    class HeadingSensor {
        -_sim
        +get_observation()
    }

    class EpisodicCompassSensor {
        +get_observation()
    }

    class EpisodicGPSSensor {
        -_sim
        -_dimensionality
        +get_observation()
    }

    class ProximitySensor {
        -_sim
        -_max_detection_radius
        +get_observation()
    }

    simulator::Sensor <|-- PointGoalSensor
    simulator::Sensor <|-- ImageGoalSensor
    PointGoalSensor <|-- IntegratedPointGoalGPSAndCompassSensor
    simulator::Sensor <|-- HeadingSensor
    HeadingSensor <|-- EpisodicCompassSensor
    simulator::Sensor <|-- EpisodicGPSSensor
    simulator::Sensor <|-- ProximitySensor

    class NavigationTask {
        +overwrite_sim_config()
        -_check_episode_is_active(): bool
    }

    EmbodiedTask <|-- NavigationTask
}
```

## Utils
```plantuml
package logging {
    class HabitatLogger {

    }

    class Logger <<builtin>> {
    }

    Logger <|-- HabitatLogger
}
```

## Vectorized Environments
```plantuml
package vector_env {
    () "_make_env_fn()"
    class VectorEnv {
        +observation_spaces: List
        +number_of_episodes: List
        +action_spaces: List
        -_num_envs: int
        -_workers: List
        -_paused: List
        -_auto_reset_done: bool
        -_mp_ctx: BaseContext
        -_connection_read_fns: List
        -_connection_write_fns: List

        +num_envs()
        +current_episode()
        +count_episodes()
        +episode_over()
        +get_metrics()
        +reset()
        +reset_at()
        +step()
        +step_at()
        +async_step()
        +async_step_at()
        +wait_step()
        +wait_step_at()
        +pause_at()
        +resume_all()
        +call()
        +call_at()
        +render()
        +close()
        -_spawn_workers()
        -__worker_env()
        -_valid_start_methods()
        -_warn_cuda_tensors()
    }

    class ThreadedVectorEnv {
        -_spawn_workers()
    }

    class _ReadWrapper {
        read_fn: Callable
        rank: int
        is_waiting: bool
    }

    class _WriteWrapper {
        write_fn: Callable
        read_wrapper: _ReadWrapper
    }
    VectorEnv <|-- ThreadedVectorEnv
    _WriteWrapper::read_wrapper -- _ReadWrapper

    note right of VectorEnv::num_envs()
        _num_envs - #_paused
    end note

    note right of VectorEnv::_warn_cuda_tensors()
        action tensor is recommenced to be a cpu tensor
    end note

    note left of ThreadedVectorEnv: easier for debugging
    note right of ThreadedVectorEnv::_spawn_workers()
        use Queue and Thread instead of Pipe and Process
    end note

}
```

## Baselines
#### PPOTrainer Procedure
1. `_init_train()`
2. `_init_envs()`
3. `_compute_actions_and_step_envs()`

```plantuml
package base_trainer {
    abstract class BaseTrainer {
        {static} supported_tasks
        -_setup_eval_config()
        +eval()
        {abstract} +train()
        {abstract} +save_checkpoint()
        {abstract} +load_checkpoint()
        {abstract} -_eval_checkpoint()
    }

    abstract class BaseRLTrainer {
        +config
        +num_updates_done
        +num_steps_done
        +flush_secs
        -_last_checkpoint_percent

        +percent_done()
        +is_done()
        +should_checkpoint()

        {static} -_pause_envs()
    }

    BaseTrainer <|-- BaseRLTrainer

    note right of BaseTrainer::eval()
        call _eval_checkpoint() defined in derived classes
    end note
}

package ppo_trainer {
    class PPOTrainer {
        +train()
        -_init_train()
        -_init_envs()
        -_compute_actions_and_step_envs()
    }

    BaseRLTrainer <|-- PPOTrainer
}

package ppo {
    class PPO {

    }
}

package environments {
    () "get_env_class()"

    class NavRLEnv {
        +reset()
        +step()
        +get_reward_range()
        +get_reward()
        +get_done()
        +get_info()
        -_episode_success()
    }
    env.RLEnv <|-- NavRLEnv
}


package rollout_storage {
    class RolloutStorage {
        +buffers: TensorDict
        +buffers[observations]
        +buffers[recurrent_hidden_states]
        +buffers[rewards]
        +buffers[value_preds]
        +buffers[returns]
        +buffers[action_log_probs]
        +buffers[actions]
        +buffers[prev_actions]
        +buffers[masks]
    }
}

package env_utils {
    () "construct_envs()"
}
```


