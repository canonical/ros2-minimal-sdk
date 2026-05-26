# ROS 2 SDK for Workshop

A streamlined development environment for ROS 2 projects. It automates ROS 2
setup, manages dependencies via `rosdep`, and persists build artefacts on the
host.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: ros2-jazzy
base: ubuntu@24.04
sdks:
  - name: ros2-minimal
    channel: jazzy/stable

actions:
  build: |
    colcon build
```

This demonstrates a basic ROS 2 build workflow with persistent build artefacts.

---

## Using the SDK

### Prerequisites, project layout

1. No prerequisite SDKs are required.
2. Clone your ROS 2 source code into your project directory (by default,
   `colcon` uses `~/workspace/src`, so no extra configuration is needed):

   ```bash
   git clone https://github.com/ros2/examples -b jazzy
   workshop shell
   colcon build
   ```

3. On launch, the SDK installs ROS 2 tools, configures `colcon`, and runs
   `rosdep install` to fetch your project's dependencies. This may take several
   minutes on first launch.

### Build the project

Once the workshop is ready:

```bash
workshop shell
colcon build
```

Build artefacts are stored in `~/workspace/` inside the workshop, mapped to
your host via the `colcon-artefacts` mount plug.

To see where the build artifacts are stored on the host:

```bash
workshop info
```

### Test and run the project

From within the workshop shell:

```bash
workshop shell
colcon test
colcon test-result --all
```

Use `ros2 run` and `ros2 launch` to execute your nodes as you would with a
standard ROS 2 installation.

---

## Plugs (resources this SDK consumes)

### `ros-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.ros`
- Purpose: Persists ROS 2 runtime configuration and log files between sessions.

### `colcon-artefacts`

- Interface: `mount`
- Workshop target: `/home/workshop/workspace` (24.04) or `/home/workshop/colcon`
  (22.04)
- Purpose: Stores `colcon` build outputs, install directories, and logs so
  builds persist across workshop updates.

### `ccache-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.cache/ccache`
- Purpose: Caches compiled objects to speed up subsequent builds.

### `gpu`

- Interface: `gpu`
- Purpose: Provides GPU pass-through for visualization tools and GPU-accelerated
  computation (e.g., Gazebo, RViz).

### `desktop`

- Interface: `desktop`
- Purpose: Enables GUI application support for ROS 2 visualization and
  simulation tools.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [ROS 2 official documentation](https://docs.ros.org/)
- [Colcon documentation](https://colcon.readthedocs.io/)
- [Canonical Robotics](https://canonical-robotics.readthedocs-hosted.com)
- [Workshop documentation](https://canonical-workshop.readthedocs-hosted.com/latest/)

---

## Community and support

- ROS community forum: [ROS Discourse](https://discourse.ros.org)
- Workshop forum:
  [Workshop Discourse](https://discourse.canonical.com/c/engineering/sdk/34)
- Please review our
  [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct) before
  participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See `CONTRIBUTING.md` for guidelines.
- Open issues or pull requests on the official repository.

---

## License and copyright

Copyright 2025 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under
the terms of the
[GNU General Public License version 3 (GPLv3)](https://www.gnu.org/licenses/gpl-3.0.html)
as published by the Free Software Foundation.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.
