---
title: Base code
parent: Tutorial
nav_order: 2
---

# Base code

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## RAII(Resource Acquisition Is Initialization)
C++에서 자원의 획득과 해제를 객체의 생명주기와 함께 관리하는 기법.
new와 같은 메모리 할당 연산자를 호출하고 delete 와 같은 메모리 해제 연산자 호출을 깜빡해서 메모리 누수가 발생한다.
{: .no_toc .fs-3 .fw-300 }

### RAII의 핵심 원칙
 - 자원을 생성자(Constructor)에서 획득
 - 자원을 소멸자(Destructor)에서 해제
 - 객체가 범위를 벗어나면 자동으로 자원이 해제됨 (RAII 원칙에 의해)

``` c++
class Resource {
public:
    // 생성자에서 메모리 할당
    Resource(val) : resource(val) { resource = new int(val);}
    // 소멸자에서 메모리 할당 해제 
    ~Resource() { delete resource; }

private:
    int* resource { nullptr };
};
int main() {
    Resource r; // 생성자에서 메모리 할당
    return 0;
} // 소멸자가 호출되면서 Resource 클래스 내에 자원이 할당 해제됨.
```

## 기본 코드
Vulkan Tutorial 에서도 RAII 기법을 사용해서 Vulkan Object의 메모리 관리를 할거라고 한다.
{: .fs-3 .fw-300 }

### Vulkan 리소스
 - vkCreateXXX : 리소스 생성
 - vkDestroyXXX and vkFreeXXX : 리소스 해제
 - vkAllocateXXX : 메모리 Allocator 리소스 할당하거나 해제 할 때 어떤 Allocator를 사용할지 정할 수가 있음.

``` c++
#define GLFW_INCLUDE_VULKAN
#include <GLFW/glfw3.h>

#include <iostream>
#include <stdexcept>
#include <cstdlib>

class HelloTriangleApplication {
public:
    void run() {
        initWindow();
        initVulkan();
        mainLoop();
        cleanup();
    }

private:
    GLFWwindow* window;

    void initWindow() {
        // glfw library 를 초기화 한다.
        glfwInit();

        // glfw 는 기본적으로 graphics api 로 opengl을 사용하도록 되어있어서 아래와 같이 NO_API을 전달
        glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API);
        glfwWindowHint(GLFW_RESIZABLE, GLFW_FALSE);

        // share : OpenGL 컨텍스트 공유 여부
        window = glfwCreateWindow(WIDTH, HEIGHT, "Vulkan", nullptr, /*share*/nullptr);
    }
    void initVulkan() {}
    void mainLoop() {
        while (!glfwWindowShouldClose(window)) {
            glfwPollEvents();
        }
    }

    void cleanup() {
        glfwDestroyWindow(window);
        glfwTerminate();
    }
};

int main() {
    HelloTriangleApplication app;

    try {
        app.run();
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
        return EXIT_FAILURE;
    }

    return EXIT_SUCCESS;
}
```

### 의문점
- InitVulkan 에서 Exception 이 난다면 cleanup 함수가 호출 안되는거 아닌가?
  - 테스트 결과 cleanup 호출이 불리지 않는데 catch 내로도 들어오지 않는다. -> Visual Studio로 다시 해봐야겠다.

### 기타 지식
- Off-Screen Rendering
  - 화면에 직접 출력하지 않고 메모리(프레임버퍼)에 렌더링하는 기술.
  - 버퍼에 렌더링하고 해당 버퍼를 활용해서 PostProcess 나 Multi-pass Rendering 등등의 기술을 적용할 수 있다.

## 요약
 - RAII를 사용하자.
 - Vulkan 리소스 생성, 삭제를 기억하자 (vkCreateXXX, vkDestroyXXX, vkDestroyXXX)
 - Vulkan 리소스 생성, 삭제시 메모리 할당자를 지정할 수 있다. (vkAllocateXXX)
 - GLFW는 기본적으로 OpenGL를 기본 API로 선택한다.

## 참고
 - [https://docs.vulkan.org/tutorial/latest/00_Introduction.html](https://docs.vulkan.org/tutorial/latest/00_Introduction.html)