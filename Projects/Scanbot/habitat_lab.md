# Habitat Lab

## Baselines

```plantuml
package base_trainer {
    class BaseTrainer {
        {static} supported_tasks
        -_setup_eval_config()
        +eval()
        {abstract} +train()
        {abstract} +save_checkpoint()
        {abstract} +load_checkpoint()
        {abstract} -_eval_checkpoint()
    }

    class BaseRLTrainer {
        +config
        +num_updates_done
        +num_steps_done
        +flush_secs
        -_last_checkpoint_percent

        {abstract} +train()
        +percent_done()
        +is_done()
        +should_checkpoint()
        {abstract} +save_checkpoint()
        {abstract} +load_checkpoint()
        {abstract} -_eval_checkpoint()

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

## Tasks
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
        +observation_spaces
        +number_of_episodes
        +action_spaces
        +num_envs
        -_workers
        -_auto_reset_done
        -_mp_ctx
        -_connection_read_fns
        -_connection_write_fns

        -_spawn_workers()
        -_valid_start_methods()
    }

    class ThreadedVectorEnv {
        -_spawn_workers()
    }

    VectorEnv <|-- ThreadedVectorEnv
}
```
