# My-Tensorflow-Needs

> **Warning** This repository is only for me to keep a few info.

I'm using a `Nvidia GPU` and I'm a `Visual Studio` user.

Lib [download](https://www.tensorflow.org/install/lang_c#download_and_extract)<br>Cuda [download](https://developer.nvidia.com/cuda-toolkit-archive)<br>cuDDN [download](https://developer.nvidia.com/rdp/cudnn-download) | [download older](https://developer.nvidia.com/rdp/cudnn-archive)

Setup `VC++ Directories`(`Include Directories` and `Library Directories`) then `Linker Input`(`tensorflow.lib`)

Then everything should be ready.

A really basic test script:

```c++
#include <format>
#include <iostream>
#include <tensorflow/c/c_api.h>

using namespace std;

TF_Status* status;
TF_SessionOptions* options;
TF_Graph* graph;
TF_Session* session;

#pragma region initAndCleanup
void init() {
    status = TF_NewStatus();
    options = TF_NewSessionOptions();
    graph = TF_NewGraph();
    session = TF_NewSession(graph, options, status);
}

void cleanup() {
    TF_CloseSession(session, status);
    TF_DeleteSession(session, status);
    TF_DeleteSessionOptions(options);
    TF_DeleteGraph(graph);
    TF_DeleteStatus(status);
}
#pragma endregion

int main() {
    std::cout << format("Tensorflow Version: {0}\n\nIf no error or missing thing appear you can continue.\n", TF_Version());
    system("pause & cls");
    // Initialize the TensorFlow library
    
    init();
    
    if (TF_GetCode(status) != TF_OK) {
        std::cerr << format("Failed to initialize TensorFlow: {0}\n", TF_Message(status));
        return 1;
    }
    std::cout << "TensorFlow initialized successfully" << std::endl;

    // Use the TensorFlow session...
    // ...

    // Clean up the TensorFlow session
    cleanup();

    system("pause");

    return 0;
}
```
