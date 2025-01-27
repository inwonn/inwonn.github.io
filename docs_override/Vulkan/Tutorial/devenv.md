---
title: Development environment
parent: Tutorial
nav_order: 1
---

# Development environment
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 개발 환경 설정
 - CMake 빌드 시스템을 활용하여 개발환경을 설정합니다.
{: .no_toc .fs-3 .fw-300 }

### **폴더 구조**

{: .lh-0  }
```
┌─ Vulkan
├─ Libraries
    ├─ glfw
    ├─ tinyobjloader
        ├─ tinyobjloader.h
    ├─ stb
    ├─ glfw3Config.cmake
    ├─ glmConfig.cmake
    └─ tinyobjloaderConfig.cmake
└─ Vulkan-Tutorial
```

### **준비물**
github 링크들은 zip파일을 다운 받거나 clone 해도 됨
{: .no_toc .fs-3 .fw-300 }
 - CMake : [https://cmake.org/download/](https://cmake.org/download/)
 - GLFW : [https://github.com/glfw/glfw/releases](https://github.com/glfw/glfw/releases)
 - tinyobjloader : [https://github.com/tinyobjloader/tinyobjloader/releases](https://github.com/tinyobjloader/tinyobjloader/releases) (tiny_obj_load.h 만 받음)
 - stb : [https://github.com/nothings/stb](https://github.com/nothings/stb)
 - Vulkan SDK : [https://vulkan.lunarg.com/sdk/home](https://vulkan.lunarg.com/sdk/home/)
   - glm 포함 ![](../../../../assets/images/Vulkan/Vulkan-Tutorial/devenv/VulkanSDK_Setup_SelectComponents.jpg)

### **Setup**

1. [Vulkan-Tutorial] 을 받습니다.
 ```
 git clone https://github.com/KhronosGroup/Vulkan-Tutorial.git
 ```
 받고 난 후 `Vulkan-Tutorial/attachments/CMakeList.txt` 파일에 [runtime exception 수정](https://github.com/inwonn/Vulkan-Tutorial/commit/a772a715f0e180ad266ab2510fef29bcf5f42ff4) 내용을 적용합니다.

2. glfw3Config.cmake, glmConfig.cmake, tinyobjloaderConfig.cmake 파일 추가
```
# glfw3Config.cmake
set(GLFW3_INCLUDE_DIR "D:/Git/Vulkan/Libraries/glfw/include/")
set(GLFW3_LIBRARY_DIR "D:/Git/Vulkan/Libraries/glfw/lib-vc2022/")
include_directories(${GLFW3_INCLUDE_DIR})
link_directories(${GLFW3_LIBRARY_DIR})
```
```
# glm3Config.cmake
add_library(glm::glm INTERFACE IMPORTED)
```
```
# tinyobjloaderConfig.cmake
set(TINYOBJLOADER_INCLUDE_DIRS "D:/Git/Vulkan/Libraries/tinyobjloader/")
include_directories(${TINYOBJLOADER_INCLUDE_DIRS})
add_library(tinyobjloader::tinyobjloader INTERFACE IMPORTED)
```

3. CMake
 - CMake 실행
   - `Where is source code` 설정 후 `Add Entry` 추가
   ![](../../../../assets/images/Vulkan/Vulkan-Tutorial/devenv/CMake_Add_Entry.jpg)
 - Configure, Generate 버튼 차례로 클릭 (Configure 눌렀을 때 빨갛게 뜨면 한번 더 누르면 됨.)
   ![](../../../../assets/images/Vulkan/Vulkan-Tutorial/devenv/CMake_Configure_Generate.jpg)

4. VisualStudio 솔루션 실행 및 빌드
 - CMake 에 의해 생성된 `Vulkan/Vulkan-Tutorial.VS2022/VulkanTutorial.sln` 을 열고 빌드한다.
   ![](../../../../assets/images/Vulkan/Vulkan-Tutorial/devenv/BuildSuccess.jpg)

## 요약
 - 괜히 CMake 로 하려다 엄청 고생했다..

## 참고
 - [https://docs.vulkan.org/tutorial/latest/02_Development_environment.html](https://docs.vulkan.org/tutorial/latest/02_Development_environment.html)

[Vulkan-Tutorial]: https://github.com/KhronosGroup/Vulkan-Tutorial