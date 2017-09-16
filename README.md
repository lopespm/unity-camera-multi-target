# Dynamic Multi Target Camera for Unity

Concise Unity library which dynamically keeps a set of objects (e.g. players and important objects) in view, a common problem for a wide range of games. 

The library was developed for, and used by my first Steam game, [Survival Ball](https://survivalball.com/). The game has an heavy shared screen local co-op component, which requires the camera to dynamically keep many key elements in view.

More information about the library's inner workings and underlying math is available in the related [blog article](https://lopespm.github.io/libraries/games/2018/12/27/camera-multi-target.html)

<img src="https://user-images.githubusercontent.com/3640622/50427667-19165c80-08a6-11e9-9306-6d05f7477262.jpg" alt="Camera Multi Target Example Scene Screenshot">

[<img src="https://user-images.githubusercontent.com/3640622/50427650-c2108780-08a5-11e9-9db0-d69e9fa329c1.gif" alt="Camera Multi Target Example Scene Video">](https://www.youtube.com/watch?v=In3eVapQ5mk) 


## Install

### By importing CameraMultiTarget.unitypackage

The pre-built package can be downloaded from the repository's releases [here](https://github.com/lopespm/unity-camera-multi-target/releases/latest). After downloading the package, import it to your project via Unity Editor: *Assets -> Import Package -> Custom Package..*.

### Or by cloning this repository

#### Clone entire repository (git)

This repository contains the complete Unity project which includes the library and an example usage scene. After you clone the entire repository using git, copy the *Assets/CameraMultiTarget* folder to your project

    git clone https://github.com/lopespm/unity-camera-multi-target.git

#### Checkout specific features (SVN)

Since cloning a specific folder can be a quite convoluted process via git, you can checkout the *Assets/CameraMultiTarget* folder directly to your project using SVN:

    cd <your_project_root_folder>
    svn checkout https://github.com/lopespm/unity-camera-multi-target/trunk/Assets/CameraMultiTarget Assets/CameraMultiTarget

Or if you wish to only install the library without the example scene:

    cd <your_project_root_folder>
    svn checkout https://github.com/lopespm/unity-camera-multi-target/trunk/Assets/CameraMultiTarget/Library Assets/CameraMultiTarget/Library


## Usage

Add the [`CameraMultiTarget`](Assets/CameraMultiTarget/Library/CameraMultiTarget.cs) component to a camera and then you can programatically set which game objects the camera will track via the component's [`SetTargets(GameObject[] targets)`](Assets/CameraMultiTarget/Library/CameraMultiTarget.cs#L23) method.

For example, you can set the targets in your game controller component (if you choose to have one), like the following:

    public class ExampleGameController : MonoBehaviour
    {
        public CameraMultiTarget cameraMultiTarget;
    
        private void Start() {
            var targets = new List<GameObject>();
            targets.Add(CreateTarget());
            targets.Add(CreateTarget());
            targets.Add(CreateTarget());
            cameraMultiTarget.SetTargets(targets.ToArray());
        }

        private GameObject CreateTarget() {
            GameObject target = GameObject.CreatePrimitive(PrimitiveType.Capsule);
            target.transform.position = Random.insideUnitSphere * 10f;
            return target;
        }
    }


## Example Scene

An example scene of the library's usage is included in this repository and in the pre-built package located in the repository's releases.