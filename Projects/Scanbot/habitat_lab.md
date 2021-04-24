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

## Environment
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
}
```

## Simulator
```plantuml
package simulator {
    class Simulator {
        sensor_suite
        action_space

        +reset()
        +step()
        +seed()
        +reconfigure()
        +geodesic_distance()
        +get_agent_state()
        +get_observation_at()
        +sample_navigable_point()
        +is_navigable()
        +action_space_shortest_path()
        +get_straight_shortest_path_points()
        +up_vector()
        +forward_vector()
        +render()
        +close()
        +previous_step_collided()
        +__enter__()
        +__exit__()
    }

    class AgentState {
        position
        rotation
    }

    class ShortestPathPoint {
        position
        rotation
        action
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
```plantuml
package embodied_task {
    class Measure {
        reset_metric()
        update_metric()
        get_metric()
        uuid
        _metric
    }

    note right of Measure::reset_metric()
        called from env.Env on reset()
    end note

    note right of Measure::update_metric()
        called from env.Env on step()
    end note

    class Metrics {
        dict
    }

    class Measurements {
        +reset_measures()
        +update_measures()
        +get_metrics() : Metrics
        +check_measure_dependencies()
        -_get_measure_index()
        measures
    }

    Measurements "1" *-- "*" Measure
    Measurements::get_metrics -> Metrics

    note left of Measurements::reset_measures()
        call all measure.reset_metric()
    end note

    note left of Measurements::update_measures()
        call all measure.update_metric()
    end note

    note left of Measurements::check_measure_dependencies()
        one measure can depend on other measures
    end note

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
    }

    BaseRLTrainer <|-- PPOTrainer
    note right of PPOTrainer::train()
        * _init_train()
        * _init_envs()
    end note
}

package env_utils {
    () "construct_envs()"
}
```
