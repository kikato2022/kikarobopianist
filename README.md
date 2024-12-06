# KikaRoboPianist: Kikato’s Dexterous Piano Playing with Deep Reinforcement Learning


KikaRoboPianist is a new benchmarking suite for high-dimensional control, targeted at testing high spatial and temporal precision, coordination, and planning, all with an underactuated system frequently making-and-breaking contacts. The proposed challenge is *mastering the piano* through bi-manual dexterity, using a pair of simulated anthropomorphic robot hands.

This codebase contains software and tasks for the benchmark, and is powered by [MuJoCo](https://mujoco.org/).

## Installation

KikaRoboPianist is supported on windows and can be installed with Python >= 3.8. We recommend using [Miniconda](https://docs.conda.io/en/latest/miniconda.html) to manage your Python environment.

Start by cloning the repository:

```bash
git clone https://github.com/kikato2022/kikarobopianist.git && cd kikarobopianist
```

Install submodule:

```bash
git submodule init && git submodule update
```

Copy shadow_hand menagerie model to kikarobopianist：

```
cd third_party/mujoco_menagerie
git checkout 1afc8be64233dcfe943b2fe0c505ec1e87a0a13e
cd ../..
mkdir -p kikarobopianist/models/hands/third_party/shadow_hand
cp -r third_party/mujoco_menagerie/shadow_hand/* kikarobopianist/models/hands/third_party/shadow_hand
```

Install **fluidsynth**:

```
goto to https://github.com/FluidSynth/fluidsynth/releases
Find the latest release and download the precompiled Windows binaries (usually in .zip format).
Extract the files to a folder.
Add the bin folder from the extracted files to your system’s PATH environment variable so you can access fluidsynth from the command line.
```

Install **PortAudio**:

```
git clone https://github.com/PortAudio/portaudio.git && cd protaudio
mkdir build
cd build
cmake .. -G "Visual Studio 16 2019"   # Replace with your version of Visual Studio
cmake --build . --config Release
Link the generated portaudio.lib or .dll files to your project.
```

Install **FFmpeg**:

```
go to https://ffmpeg.org/download.html and select a Windows build.
Download and extract the .zip file to a directory of your choice (e.g., C:\ffmpeg).
Add FFmpeg to System PATH:
	Open Control Panel > System > Advanced system settings.
	Click Environment Variables.
	Under System variables, select Path and click Edit.
	Add the bin folder inside the extracted FFmpeg directory (e.g., C:\ffmpeg\bin).
open a command prompt and run : ffmpeg -version
```

Install **soundfonts**：

```
mkdir -p third_party/soundfonts

# Salamander Grand Piano.
LINK=https://freepats.zenvoid.org/Piano/SalamanderGrandPiano/SalamanderGrandPiano-SF2-V3+20200602.tar.xz
wget $LINK
unzip: SalamanderGrandPiano-SF2-V3+20200602.tar.xz
Move-Item "SalamanderGrandPiano-SF2-V3+20200602\SalamanderGrandPiano-V3+20200602.sf2" "third_party\soundfonts\SalamanderGrandPiano.sf2"
Remove-Item -Recurse -Force "SalamanderGrandPiano-SF2-V3+20200602"
Remove-Item -Force "SalamanderGrandPiano-SF2-V3+20200602.tar.xz"

# Make a copy of the soundfonts in robopianist/soundfonts.
mkdir -p kikarobopianist/soundfonts
Copy-Item -Recurse -Force "third_party/soundfonts/*" "kikarobopianist/soundfonts"
```



Finally, create a new conda environment and install RoboPianist in editable mode:

```bash
conda create -n pianist python=3.10
conda activate pianist

pip install -e ".[dev]"
```

To test your installation, run `make test` and verify that all tests pass.

### Optional: Download additional soundfonts

We recommend installing additional soundfonts to improve the quality of the synthesized audio. You can easily do this using the RoboPianist CLI:

```bash
kikarobopianist soundfont --download
```

For more soundfont-related commands, see [docs/soundfonts.md](docs/soundfonts.md).

## MIDI Dataset

The PIG dataset cannot be redistributed on GitHub due to licensing restrictions. See [docs/dataset](docs/dataset.md) for instructions on where to download it and how to preprocess it.

## CLI

KikaRoboPianist comes with a command line interface (CLI) that can be used to download additional soundfonts, play MIDI files, preprocess the PIG dataset, and more. For more information, see [docs/cli.md](docs/cli.md).

## License and Disclaimer

[MuJoco Menagerie](https://github.com/deepmind/mujoco_menagerie)'s license can be found [here](https://github.com/deepmind/mujoco_menagerie/blob/main/LICENSE). Soundfont licensing information can be found [here](docs/soundfonts.md). MIDI licensing information can be found [here](docs/dataset.md). All other code is licensed under an [Apache-2.0 License](LICENSE).

This is not an officially supported Google product.
