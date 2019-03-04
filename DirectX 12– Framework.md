# [3D Game Engine Programming](https://www.3dgep.com/)

## Helping you build your dream game engine

[![](https://www.3dgep.com/wp-content/uploads/2017/12/Microsoft-DirectX-12.png)](https://www.3dgep.com/)Search

### Main menu

[Skip to primary content](https://www.3dgep.com/learning-directx12-3/#content)

-   [Home](https://www.3dgep.com/)
-   [Math](https://www.3dgep.com/category/math/)
-   [Unity](https://www.3dgep.com/category/unity/)
-   [Graphics Programming](https://www.3dgep.com/category/graphics-programming/)
-   [CUDA](https://www.3dgep.com/category/cuda/)
-   [About](https://www.3dgep.com/about-3d-game-engine-programming/)

### Post navigation

[←  Previous](https://www.3dgep.com/learning-directx12-2/)

# Learning DirectX 12 – Lesson 3 – Framework

Posted on [June 8, 2018](https://www.3dgep.com/learning-directx12-3/ "2:34 pm") by [Jeremiah](https://www.3dgep.com/author/jeremiah/ "View all posts by Jeremiah")

[![DirectX 12](https://www.3dgep.com/wp-content/uploads/2017/12/DirectX-12-Logo-150x150.png)](https://www.3dgep.com/wp-content/uploads/2017/12/DirectX-12-Logo.png)

DirectX 12 – Lesson 3

In this tutorial, you will be introduced to several classes that will help you to create a robust and flexible framework for building DirectX 12 applications. Some of the problems that are solved with the classes introduced in this lesson are managing CPU descriptors, copying CPU descriptors to GPU visible descriptor heaps, managing resource state across multiple threads, and uploading dynamic buffer data to the GPU. To automatically manage the state and descriptors for resources, a custom command list class is also provided.

Contents  [[hide](https://www.3dgep.com/learning-directx12-3/#)]

-   [1  Introduction](https://www.3dgep.com/learning-directx12-3/#Introduction)
-   [2  Upload Buffer](https://www.3dgep.com/learning-directx12-3/#Upload_Buffer)
    -   [2.1  UploadBuffer Class](https://www.3dgep.com/learning-directx12-3/#UploadBuffer_Class)
        -   [2.1.1  UploadBuffer Header](https://www.3dgep.com/learning-directx12-3/#UploadBuffer_Header)
        -   [2.1.2  UploadBuffer Preamble](https://www.3dgep.com/learning-directx12-3/#UploadBuffer_Preamble)
        -   [2.1.3  UploadBuffer::UploadBuffer](https://www.3dgep.com/learning-directx12-3/#UploadBufferUploadBuffer)
        -   [2.1.4  UploadBuffer::Allocate](https://www.3dgep.com/learning-directx12-3/#UploadBufferAllocate)
        -   [2.1.5  UploadBuffer::RequestPage](https://www.3dgep.com/learning-directx12-3/#UploadBufferRequestPage)
        -   [2.1.6  UploadBuffer::Reset](https://www.3dgep.com/learning-directx12-3/#UploadBufferReset)
        -   [2.1.7  UploadBuffer::Page::Page](https://www.3dgep.com/learning-directx12-3/#UploadBufferPagePage)
        -   [2.1.8  UploadBuffer::Page::~Page](https://www.3dgep.com/learning-directx12-3/#UploadBufferPagePage-2)
        -   [2.1.9  UploadBuffer::Page::HasSpace](https://www.3dgep.com/learning-directx12-3/#UploadBufferPageHasSpace)
        -   [2.1.10  UploadBuffer::Page::Allocate](https://www.3dgep.com/learning-directx12-3/#UploadBufferPageAllocate)
        -   [2.1.11  UploadBuffer::Page::Reset](https://www.3dgep.com/learning-directx12-3/#UploadBufferPageReset)
-   [3  Descriptor Allocator](https://www.3dgep.com/learning-directx12-3/#Descriptor_Allocator)
    -   [3.1  DescriptorAllocator Class](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocator_Class)
        -   [3.1.1  DescriptorAllocator Header](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocator_Header)
        -   [3.1.2  DescriptorAllocator Preamble](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocator_Preamble)
        -   [3.1.3  DescriptorAllocator::DescriptorAllocator](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorDescriptorAllocator)
        -   [3.1.4  DescriptorAllocator::CreateAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorCreateAllocatorPage)
        -   [3.1.5  DescriptorAllocator::Allocate](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorAllocate)
        -   [3.1.6  DescriptorAllocator::ReleaseStaleDescriptors](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorReleaseStaleDescriptors)
    -   [3.2  DescriptorAllocatorPage Class](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)
        -   [3.2.1  DescriptorAllocatorPage Header](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Header)
        -   [3.2.2  DescriptorAllocatorPage Preamble](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Preamble)
        -   [3.2.3  DescriptorAllocatorPage::DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageDescriptorAllocatorPage)
        -   [3.2.4  DescriptorAllocatorPage::GetHeapType](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageGetHeapType)
        -   [3.2.5  DescriptorAllocatorPage::NumFreeHandles](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageNumFreeHandles)
        -   [3.2.6  DescriptorAllocatorPage::HasSpace](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageHasSpace)
        -   [3.2.7  DescriptorAllocatorPage::AddNewBlock](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageAddNewBlock)
        -   [3.2.8  DescriptorAllocatorPage::Allocate](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageAllocate)
        -   [3.2.9  DescriptorAllocatorPage::ComputeOffset](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageComputeOffset)
        -   [3.2.10  DescriptorAllocatorPage::Free](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageFree)
        -   [3.2.11  DescriptorAllocatorPage::FreeBlock](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageFreeBlock)
        -   [3.2.12  DescriptorAllocatorPage::ReleaseStaleDescriptors](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageReleaseStaleDescriptors)
    -   [3.3  DescriptorAllocation Class](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Class)
        -   [3.3.1  DescriptorAllocation Header](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Header)
        -   [3.3.2  DescriptorAllocation Preamble](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Preamble)
        -   [3.3.3  DescriptorAllocation Default Constructor](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Default_Constructor)
        -   [3.3.4  DescriptorAllocation Parameratized Constructor](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Parameratized_Constructor)
        -   [3.3.5  DescriptorAllocation Destructor](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Destructor)
        -   [3.3.6  DescriptorAllocation Move Constructor](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Move_Constructor)
        -   [3.3.7  DescriptorAllocation Move Assignment](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Move_Assignment)
        -   [3.3.8  DescriptorAllocation::Free](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocationFree)
        -   [3.3.9  DescriptorAllocation::IsNull](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocationIsNull)
        -   [3.3.10  DescriptorAllocation::GetDescriptorHandle](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocationGetDescriptorHandle)
        -   [3.3.11  DescriptorAllocation::GetNumHandles](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocationGetNumHandles)
        -   [3.3.12  DescriptorAllocation::GetDescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocationGetDescriptorAllocatorPage)
-   [4  Dynamic Descriptor Heap](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)
    -   [4.1  DynamicDescriptorHeap Class](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeap_Class)
        -   [4.1.1  DynamicDescriptorHeap Header](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeap_Header)
        -   [4.1.2  DynamicDescriptorHeap Preamble](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeap_Preamble)
        -   [4.1.3  DynamicDescriptorHeap::DynamicDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapDynamicDescriptorHeap)
        -   [4.1.4  DynamicDescriptorHeap::ParseRootSignature](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapParseRootSignature)
        -   [4.1.5  DynamicDescriptorHeap::StageDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapStageDescriptors)
        -   [4.1.6  DynamicDescriptorHeap::ComputeStaleDescriptorCount](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapComputeStaleDescriptorCount)
        -   [4.1.7  DynamicDescriptorHeap::RequestDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapRequestDescriptorHeap)
        -   [4.1.8  DynamicDescriptorHeap::CreateDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCreateDescriptorHeap)
        -   [4.1.9  DynamicDescriptorHeap::CommitStagedDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptors)
        -   [4.1.10  DynamicDescriptorHeap::CommitStagedDescriptorsForDraw](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptorsForDraw)
        -   [4.1.11  DynamicDescriptorHeap::CommitStagedDescriptorsForDispatch](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptorsForDispatch)
        -   [4.1.12  DynamicDescriptorHeap::CopyDescriptor](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCopyDescriptor)
        -   [4.1.13  DynamicDescriptorHeap::Reset](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapReset)
-   [5  Resource State Tracking](https://www.3dgep.com/learning-directx12-3/#Resource_State_Tracking)
    -   [5.1  ResourceStateTracker Class](https://www.3dgep.com/learning-directx12-3/#ResourceStateTracker_Class)
        -   [5.1.1  ResourceStateTracker Header](https://www.3dgep.com/learning-directx12-3/#ResourceStateTracker_Header)
        -   [5.1.2  ResourceStateTracker Preamble](https://www.3dgep.com/learning-directx12-3/#ResourceStateTracker_Preamble)
        -   [5.1.3  ResourceStateTracker::ResourceBarrier](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerResourceBarrier)
        -   [5.1.4  ResourceStateTracker::TransitionResource](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerTransitionResource)
        -   [5.1.5  ResourceStateTracker::UAVBarrier](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerUAVBarrier)
        -   [5.1.6  ResourceStateTracker::AliasBarrier](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerAliasBarrier)
        -   [5.1.7  ResourceStateTracker::FlushResourceBarriers](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerFlushResourceBarriers)
        -   [5.1.8  ResourceStateTracker::FlushPendingResourceBarriers](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerFlushPendingResourceBarriers)
        -   [5.1.9  ResourceStateTracker::CommitFinalResourceStates](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerCommitFinalResourceStates)
        -   [5.1.10  ResourceStateTracker::Reset](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerReset)
        -   [5.1.11  ResourceStateTracker::Lock](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerLock)
        -   [5.1.12  ResourceStateTracker::Unlock](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerUnlock)
        -   [5.1.13  ResourceStateTracker::AddGlobalResourceState](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerAddGlobalResourceState)
        -   [5.1.14  ResourceStateTracker::RemoveGlobalResourceState](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerRemoveGlobalResourceState)
-   [6  Custom Command List](https://www.3dgep.com/learning-directx12-3/#Custom_Command_List)
    -   [6.1  CommandList Class](https://www.3dgep.com/learning-directx12-3/#CommandList_Class)
        -   [6.1.1  CommandList::TransitionBarrier](https://www.3dgep.com/learning-directx12-3/#CommandListTransitionBarrier)
        -   [6.1.2  CommandList::CopyResource](https://www.3dgep.com/learning-directx12-3/#CommandListCopyResource)
        -   [6.1.3  CommandList::SetGraphicsDynamicConstantBuffer](https://www.3dgep.com/learning-directx12-3/#CommandListSetGraphicsDynamicConstantBuffer)
        -   [6.1.4  CommandList::SetShaderResourceView](https://www.3dgep.com/learning-directx12-3/#CommandListSetShaderResourceView)
        -   [6.1.5  CommandList::Draw](https://www.3dgep.com/learning-directx12-3/#CommandListDraw)
-   [7  Conclusion](https://www.3dgep.com/learning-directx12-3/#Conclusion)
-   [8  Download the Source](https://www.3dgep.com/learning-directx12-3/#Download_the_Source)
-   [9  References](https://www.3dgep.com/learning-directx12-3/#References)

This lesson is very heavy on C++ source code and may be difficult to digest for some readers. I feel it is necessary to show the implementation details of these classes here before going on to later lessons since they are used to create the demos in those lessons. Without some introduction to these classes, the reader may feel lost or frustrated if they don’t understand how the demos are built if they don’t see the underlying source code.

The design of these classes prioritizes convenience for the graphics programmer when creating demos (for research purposes ) but may not reflect the most optimized implementations that would be used in production game engines. Feel free to share your thoughts in the comments below about how to improve the design of the classes shown here.  

# Introduction

As you have learned in the previous lessons, compared to DirectX 11 or OpenGL, DirectX 12 introduces a few architectural changes that creates some challenges for the graphics programmer. These architectural changes provide a lower-level rendering API but also require a lot of additional code to be written just to get anything to appear on screen. When I first started working with DirectX 12, I really struggled with issues such as memory management, descriptors, and resource state management. What’s the best memory management scheme to use to store resources? How do I make sure I have enough descriptors to render a frame?

In this lesson, I will introduce several classes that will greatly simplify the development of DirectX 12 applications. The first of these classes is the  `UploadBuffer`. The  `UploadBuffer`  is a  _linear allocator_  that creates resources in an  _Upload Heap_. The purpose of this class is to provide the ability to upload dynamic constant, vertex, and index buffer data (or any buffer data for that matter) to the GPU. The most common use-case for the  `UploadBuffer`  class is to upload uniform data to a  `ConstantBuffer`used in a shader. Another typical use-case for the  `UploadBuffer`  is for particle effects. If the particles are simulated on the CPU, the computed particle attributes need to be uploaded to the GPU every frame. Instead of creating a new upload buffer every frame, the  `UploadBuffer`  is used to upload the particle data to the GPU. Another use-case for the  `UploadBuffer`  is rendering a  **User Interface**  (**UI**). If the UI is dynamic (for example if you want to show run-time performance profiling) then the UI needs to be generated every frame with the new output. For each of these use cases, it is ideal to create a large resource in an upload heap, map a CPU pointer to the underlying resource, and copy the required data (using a  `[memcpy](http://en.cppreference.com/w/cpp/string/byte/memcpy)`  for example).

The next class that I will discuss is the  `DescriptorAllocator`  class that is used to allocate a number of CPU visible descriptors. CPU visible descriptors are used for  **Render Target Views**  (**RTV**) and  **Depth-Stencil Views**  (**DSV**). CPU visible descriptors are also used to create  **Constant Buffer Views**  (**CBV**),  **Shader Resource Views**(**SRV**),  **Unordered Access Views**  (**UAV**), and creating  **Samplers**  but CBVs, SRVs, UAVs, and Samplers require a corresponding GPU visible descriptor before they can be used in a shader.

Whenever a  `Draw`  or  `Dispatch`  command is executed on a command list, any resource that is read from or written to in the shader needs to be bound to the graphics or compute pipeline using a GPU visible descriptor. Although buffer resources can be bound to the GPU using  _inline descriptors_  (see  [Lesson 2](https://www.3dgep.com/learning-directx12-2/)), texture resources cannot be bound using inline descriptors and  _must_  be bound to the GPU using a descriptor table. If the shader uses a lot of textures (this is the case if you are doing  _Physically Based Rendering_  for example), then all of the textures needed during the draw or dispatch call must be bound to the graphics, or compute pipelines at the same time. Usually all of the SRV’s for the textures are bound in a contiguous block of GPU visible descriptors in a single descriptor table range. But if textures are loaded in random order, or the same texture is being used for multiple draw calls then how can one ensure that all of the textures are bound in a contiguous block of GPU visible descriptors? Another issue is that only a single descriptor heap of the same type (`[CBV_SRV_UAV](https://msdn.microsoft.com/en-us/library/dn859379(v=vs.85).aspx)`, or  `[SAMPLER](https://msdn.microsoft.com/en-us/library/dn859379(v=vs.85).aspx)`) can be bound on the command list at any moment. So all GPU visible descriptors must come from a single descriptor heap (the descriptor heaps can only be changed between  `Draw`or  `Dispatch`  calls)! Yet another issue arises since descriptors cannot be reused until the command list that is using them has completed executing on the GPU. So how do you know how many GPU visible descriptors need to be allocated up-front? In all but the most simple case, it is impossible to know how many GPU visible descriptors will ever be needed for an entire frame (or 3 frames in the case of triple-buffering). The  `DynamicDescriptorHeap`  class described in this lesson solves the problem of ensuring that all of the GPU visible descriptors are copied to a single GPU visible descriptor heap before a  `Draw`  or  `Dispatch`  command is executed on the GPU.

Another tricky problem to solve in a DirectX 12 renderer is ensuring that resources are always in the correct state when they need to be. In order to perform a resource transition, both the  _before_  and  _after_  states of the resource need to be specified in the transition barrier. But if a resource is being used in different states in multiple command lists, then the graphics programmer needs to know exactly what state it was used in the previous command list that was executed. A naïve approach would be to create a class that stores both the resource and the current state of that resource. Anytime a transition barrier is performed on the resource, the current resource state is checked and used as the  _before_  state. This approach would work in a single-threaded renderer but wouldn’t work if the command lists are being built on different threads! In this case, there is no way to guarantee the state of the resource across multiple threads. The graphics programmer should only be concerned with implementing the graphics application and not concerned with synchronizing the state of a resource across multiple command lists, multiple command queues, and multiple threads! The  `ResourceStateTracker`  class introduced in this lesson strives to solve the problem of tracking the resource state in a multi-threaded renderer.

In order to bring everything together and make the life of a graphics programmer as easy as possible, a custom  `CommandList`  class is introduced which uses the aforementioned classes to simplify loading of texture and buffer resources, tracking resource state and minimizing transition barriers, and ensuring that all of the resources used in a shader are correctly bound to GPU visible descriptors. The goal of the custom  `CommandList`  class described in this lesson is to abstract all of the complications of using DirectX 12 away and reduce the game specific code from thousands of lines of (user) code to just a few hundred.

# Upload Buffer

The  `UploadBuffer`  class provides a simple wrapper around a resource that is created in an  _upload heap_. The  `UploadBuffer`  is implemented as a  _linear allocator_  that allocates  _chunks_  or  _blocks_  of memory from memory  **pages**. If a memory page cannot satisfy an allocation request, a new page is created and added to a list of available pages. A linear allocator can’t grow indefinitely so when a page of memory is no longer in use (for example, the command list that uses an allocation from that page is finished executing on the GPU) then the page can be returned to the list of available pages in the heap. The image below shows an example of a linear allocator.

[![Linear Allocator](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-1-1024x461.png)](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-1.png)

The image shows two pages from a linear allocator. The green blocks are free allocations while the red blocks are allocated. The green blocks in the first page before the offset pointer represent internal fragmentation created by aligned allocations.

A linear allocator is probably the simplest allocator to implement since it only needs to store two pointers per memory page (the base pointer, and the current offset in the page). The above image shows an example of a linear allocator after several allocations have been made. The red blocks represent allocated blocks while the green blocks represent free blocks within the page. Allocated blocks are not freed or returned back to the memory page but once all of the allocations are no longer being used, then the entire page of memory can be returned to the available pages for the allocator and the offset pointer within the page is reset to the base pointer. The green chunks of free memory between the allocated blocks are a result of external fragmentation created by the alignment of allocated blocks. For example, if the first allocation is a block of 64 bytes and the next allocation needs to be aligned to 256-bytes (constant buffers are required to be aligned to 256-bytes) then there are 192 bytes of unused space in the memory page between the first and second allocations.

[![Linear Allocator (2)](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-Example-1024x208.png)](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-Example.png)

The example shows a memory page with two allocations. The first of 64 bytes and the second allocation is 256 byte aligned. This results in 192 bytes of external fragmentation between the two allocations.

The linear allocator also suffers from internal fragmentation when a block of memory is requested but the size of the allocation is smaller than the requested alignment. For example, a block of 64 bytes of memory is 256-byte aligned (this is typical of a constant buffer that contains only a single 4×4 matrix). The allocation returns 256 bytes even if only 64 bytes will ever be used.

[![](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-Internal-Fragmentation-1024x208.png)](https://www.3dgep.com/wp-content/uploads/2018/05/Linear-Allocator-Internal-Fragmentation.png)

The following image shows the result of internal fragmentation caused by allocations that are smaller than their alignment. The shaded area in the second allocation is wasted since the allocation only required 64 bytes but 256 bytes are allocated because of the alignment requirements resulting in 192 bytes of internal fragmentation.

The shaded area in the second allocation shown in the image above is unused memory resulting in internal fragmentation since only 64 bytes was allocated but it required 256 byte alignment so 192 bytes remain unused.

Regardless of the internal and external fragmentation issues, the linear allocator is ideal due to its simplicity and speed. Allocating from the linear allocator only requires the offset pointer to be updated which can be performed in constant time (O(1)O(1)).

## UploadBuffer Class

As mentioned in the introduction, the  `UploadBuffer`  class is used to satisfy requests for memory that must be uploaded to the GPU. When the data in the upload buffer is no longer required, the memory pages can be reused. A page only becomes available again when the command list that is using memory from a page of memory in the upload buffer is finished executing on the GPU. In order to simplify the implementation of the  `UploadBuffer`  class, it is assumed that each  `UploadBuffer`  instance is associated to a single command list/allocator. In the  [first tutorial](https://www.3dgep.com/learning-directx12-1/), you learned that a command allocator can’t be reset unless it is no longer “in-flight” on the command queue. Similar to the command allocator, the  `UploadBuffer`  is only reset when any memory allocations from the  `UploadBuffer`  are no longer “in-flight” on the command queue. This is shown later in this lesson when describing the custom  `CommandList`class.

The implementation of this  `UploadBuffer`  class is inspired by the implementation of the  `[LinearAllocator](https://github.com/Microsoft/DirectX-Graphics-Samples/blob/master/MiniEngine/Core/LinearAllocator.h)`  class in the MiniEngine provided with the  [DirectX-Graphics-Samples](https://github.com/Microsoft/DirectX-Graphics-Samples)repository available on  [GitHub](https://github.com/)  [[1]](https://www.3dgep.com/learning-directx12-3/#cite-1).

The  `UploadBuffer`  class provides the following functionality:

-   `Allocate`: Allocates a chunk of memory that can be used to upload data to the GPU.
-   `Reset`: Release all allocations for reuse.

This provides a very simple interface definition for the  `UploadBuffer`  class.

The header file for the  `UploadBuffer`  class is shown next.

### UPLOADBUFFER HEADER

The  `UploadBuffer`  header file defines the public, and private members of the class. The preamble is shown first which defines the header file dependencies for the class.

UploadBuffer.h

1

2

3

4

5

6

7

8

9

10

11

12

`/**`

`* An UploadBuffer provides a convenient method to upload resources to the GPU.`

`*/`

`#pragma once`

`#include <Defines.h>`

`#include <wrl.h>`

`#include <d3d12.h>`

`#include <memory>`

`#include <deque>`

The  `[Defines.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/Defines.h)`  header file included on line 6 contains a few useful macro definitions. This file is local to the project but the contents are not shown here for brevity. The source code for this file is available on GitHub here:  [Defines.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/Defines.h)

The  `[wrl.h](https://docs.microsoft.com/en-us/cpp/windows/windows-runtime-cpp-template-library-wrl)`  header file provides access to the  `[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class)`  template class.

The  `[d3d12.h](https://msdn.microsoft.com/en-us/library/dn899121(v=vs.85).aspx)`  header file contains the interfaces for the DirectX 12 API.

The  `[memory](http://en.cppreference.com/w/cpp/header/memory)`  header contains the  `[std::shared_ptr](http://en.cppreference.com/w/cpp/memory/shared_ptr)`  which is used to track the lifetime of memory pages in the allocator. The  `[deque](http://en.cppreference.com/w/cpp/header/deque)`  header contains the  `[std::deque](http://en.cppreference.com/w/cpp/container/deque)`  container class which is used to store a pool of memory pages.

UploadBuffer.h

14

15

16

17

18

19

20

21

22

`class` `UploadBuffer`

`{`

`public``:`

`// Use to upload data to the GPU`

`struct` `Allocation`

`{`

`void* CPU;`

`D3D12_GPU_VIRTUAL_ADDRESS GPU;`

`};`

The  `Allocation`  structure defined on line 18 is used to return an allocation from the  `UploadBuffer::Allocate`  method which is shown later.

UploadBuffer.h

24

25

26

27

`/**`

`* @param pageSize The size to use to allocate new pages in GPU memory.`

`*/`

`explicit` `UploadBuffer(``size_t` `pageSize = _2MB);`

The  `UploadBuffer`  class declares only a single constructor which takes the size of a memory page as its only argument. The default size of a page of memory is 2MB. 2MB should be sufficient for most cases, depending on usage. The size of a memory page should be approximately large enough to contain all of the allocations for a single command list. If a lot of dynamic memory allocations are made in the command list, then it may be worthwhile to make larger pages. It is important to understand that the memory pages are never returned to the system. Once a page is allocated, it is never deallocated unless the  `UploadBuffer`  instance is destructed. The intention of the  `UploadBuffer`  is that it is reused each frame so the same allocations will likely be made the next frame, but the data will be different. If the pages are never freed, then the cost of creating the pages each frame can be avoided.

UploadBuffer.h

31

32

33

34

`/**`

`* The maximum size of an allocation is the size of a single page.`

`*/`

`size_t` `GetPageSize()` `const` `{` `return` `m_PageSize; }`

The  `GetPageSize`  method simply returns the size of a single page of the allocator. This can be used to check if an allocation can be satisfied by the  `UploadBuffer`. If an allocation can’t be satisfied (if the page size is too small for example) then this might be an indication that the page size needs to be larger.

UploadBuffer.h

37

38

39

40

41

42

43

44

`/**`

`* Allocate memory in an Upload heap.`

`* An allocation must not exceed the size of a page.`

`* Use a memcpy or similar method to copy the`

`* buffer data to CPU pointer in the Allocation structure returned from`

`* this function.`

`*/`

`Allocation Allocate(``size_t` `sizeInBytes,` `size_t` `alignment);`

The  `Allocate`  method allocates a chunk of memory with the specified allocation. The  `Allocation`  structure returned from this method is used to copy the CPU memory into the GPU virtual address space.

UploadBuffer.h

45

46

47

48

49

`/**`

`* Release all allocated pages. This should only be done when the command list`

`* is finished executing on the CommandQueue.`

`*/`

`void Reset();`

The  `Reset`  method is used to reset any allocations so that the memory can be reused for the next frame.

To keep track of the memory pages, an internal  `Page`  struct is defined. The  `Page`  struct stores a base CPU pointer, the offset within the page, and the  `[ID3D12Resource](https://msdn.microsoft.com/en-us/library/dn788709(v=vs.85).aspx)`  that holds the GPU memory.

UploadBuffer.h

51

52

53

54

55

`private``:`

`// A single page for the allocator.`

`struct` `Page`

`{`

`Page(``size_t` `sizeInBytes);`

The  `Page`  structure has only a single constructor which takes the size of the page as its only arguments. This is the same as the  `pageSize`  argument that is passed to the constructor of the  `UplodBuffer`  class.

UploadBuffer.h

58

59

60

`// Check to see if the page has room to satisfy the requested`

`// allocation.`

`bool` `HasSpace(``size_t` `sizeInBytes,` `size_t` `alignment )` `const``;`

The  `Page::HasSpace`  method is used to check if the page can satisfy the requested allocation. If the allocation cannot be satisfied by the current page, the current page is retired and a new page is created.

UploadBuffer.h

62

63

64

65

66

`// Allocate memory from the page.`

`// Throws std::bad_alloc if the the allocation size is larger`

`// that the page size or the size of the allocation exceeds the`

`// remaining space in the page.`

`Allocation Allocate(``size_t` `sizeInBytes,` `size_t` `alignment);`

The  `Page::Allocate`  method is used to perform the actual allocation with the memory page.

UploadBuffer.h

68

69

`// Reset the page for reuse.`

`void Reset();`

The  `Page::Reset`  method is used to reset the page for reuse. This resets the offset within the page to 0.

UploadBuffer.h

71

72

73

74

75

76

77

78

79

80

81

82

83

`private``:`

`Microsoft::WRL::ComPtr<ID3D12Resource> m_d3d12Resource;`

`// Base pointer.`

`void* m_CPUPtr;`

`D3D12_GPU_VIRTUAL_ADDRESS m_GPUPtr;`

`// Allocated page size.`

`size_t` `m_PageSize;`

`// Current allocation offset in bytes.`

`size_t` `m_Offset;`

`};`

The data that is private to the  `Page`  structure is the  `[ID3D12Resource](https://msdn.microsoft.com/en-us/library/dn788709(v=vs.85).aspx)`  that contains the GPU memory for the page, the CPU and GPU base pointers, and the current offset within the page. The  `m_PageSize`  variable is also stored to make sure the requested allocation can be satisfied.

The  `UploadBuffer`  class needs to keep track of a pool of pages and provide a method to create new pages as required.

UploadBuffer.h

85

86

`// A pool of memory pages.`

`using` `PagePool = std::deque< std::shared_ptr<Page> >;`

The  `PagePool`  type alias defines a  `[std::deque](http://en.cppreference.com/w/cpp/container/deque)`  container that stores pointers to the memory pages.

UploadBuffer.h

88

89

90

`// Request a page from the pool of available pages`

`// or create a new page if there are no available pages.`

`std::shared_ptr<Page> RequestPage();`

The  `RequestPage`  private method is used to provide an available memory page if one is available. If there are no more available pages, a new one is created and added to the page pool.

UploadBuffer.h

92

93

`PagePool m_PagePool;`

`PagePool m_AvailablePages;`

The  `m_PagePool`  member variable is a  `PagePool`  used to hold all of the pages that have ever been created by the  `UploadBuffer`  class. The  `m_AvailablePages`  member variable on the other hand, is a pool of pages that are available for allocation.

UploadBuffer.h

95

96

97

98

99

100

`std::shared_ptr<Page> m_CurrentPage;`

`// The size of each page of memory.`

`size_t` `m_PageSize;`

`};`

The  `m_CurrentPage`  member variable is used to store a pointer to the current memory page. The  `m_PageSize`  variable stores the size of a memory page. This is set to the  `pageSize`  constructor argument and is used for allocating new pages.

[![Upload Buffer Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for UploadBuffer.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/UploadBuffer.h)

### UPLOADBUFFER PREAMBLE

The preamble for the source file of the  `UploadBuffer`  class contains the header file dependencies that are specific to the implementation of the class.

UploadBuffer.cpp

1

2

3

4

5

6

7

8

9

10

`#include <DX12LibPCH.h>`

`#include <UploadBuffer.h>`

`#include <Application.h>`

`#include <Helpers.h>`

`#include <d3dx12.h>`

`#include <new> // for std::bad_alloc`

The  `DX12LibPCH.h`  header file is the precompiled header file for the  `DX12Lib`  project. All of the classes described in this article are part of the  **DX12Lib**  project.

The  `UploadBuffer.h`  is the header file that was just described in the previous section.

The  `Helpers.h`  header file contains some helper functions that are used by the  `UploadBuffer`  class. The source code for this file can be retrieved here:  [Helpers.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/Helpers.h).

The  `[d3dx12.h](https://github.com/Microsoft/DirectX-Graphics-Samples/blob/master/Libraries/D3DX12/d3dx12.h)`  provides some helper functions and structs specific for DirectX 12. This file is hosted on  [GitHub](https://github.com/)  and not distributed with the Windows 10 SDK. It is good practice to check GitHub if there is a new version of this file and always use the latest version in your own projects.

The  `[new](http://en.cppreference.com/w/cpp/header/new)`  header contains the  `[std::bad_alloc](http://en.cppreference.com/w/cpp/memory/new/bad_alloc)`  exception class which is thrown if an allocation larger than the size of a page is requested.

### UPLOADBUFFER::UPLOADBUFFER

The  `UploadBuffer`  class provides a single parameterized constructor. The constructor takes the size of a memory page as its only argument.

UploadBuffer.cpp

12

13

14

`UploadBuffer::UploadBuffer(``size_t` `pageSize)`

`: m_PageSize(pageSize)`

`{}`

Besides setting the  `m_PageSize`  member variable, the constructor does nothing. Memory pages will only be allocated if an allocation is requested. The  `UploadBuffer`class is intended to be used as an internal class for the custom  `CommandList`  class (that is shown later in the lesson). If dynamic allocations are not required by the command list, then no pages will be allocated. This is a typical example of  [Lazy Initialization](https://en.wikipedia.org/wiki/Lazy_initialization).

### UPLOADBUFFER::ALLOCATE

The  `Allocate`  method is used to allocate a chunk (or block) of memory from a memory page. This method returns an  `UploadBuffer::Allocation`  struct that was defined in the header file.

UploadBuffer.cpp

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

`UploadBuffer::Allocation UploadBuffer::Allocate(``size_t` `sizeInBytes,` `size_t` `alignment)`

`{`

`if` `(sizeInBytes > m_PageSize)`

`{`

`throw` `std::bad_alloc();`

`}`

`// If there is no current page, or the requested allocation exceeds the`

`// remaining space in the current page, request a new page.`

`if` `(!m_CurrentPage || !m_CurrentPage->HasSpace(sizeInBytes, alignment))`

`{`

`m_CurrentPage = RequestPage();`

`}`

`return` `m_CurrentPage->Allocate(sizeInBytes, alignment);`

`}`

The  `Allocate`  method takes two arguments:

-   `size_t sizeInBytes`: The size of the allocation in bytes.
-   `size_t alignment`: The memory alignment of the allocation in bytes. For example, allocations for constant buffers must be aligned to 256 bytes.

If the size of the allocation exceeds the size of a memory page, the method throws a  [std::bad_alloc](http://en.cppreference.com/w/cpp/memory/new/bad_alloc)  exception.

If there is either no memory page (this is the case when the  `UploadBuffer`  is first created) or the current page cannot satisfy the request, a new page is requested.

On line 33, the actual allocation is made from the current memory page and the resulting allocation is returned to the caller.

### UPLOADBUFFER::REQUESTPAGE

If either the allocator does not have a page to make an allocation from, or the current page does not have the available space to satisfy the allocation request, a new page must be retrieved from the list of available pages or a new page must be created. The  `RequestPage`  method will return a memory page that can be used to satisfy allocation requests.

UploadBuffer.cpp

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

`std::shared_ptr<UploadBuffer::Page> UploadBuffer::RequestPage()`

`{`

`std::shared_ptr<Page> page;`

`if` `(!m_AvailablePages.empty())`

`{`

`page = m_AvailablePages.front();`

`m_AvailablePages.pop_front();`

`}`

`else`

`{`

`page = std::make_shared<Page>(m_PageSize);`

`m_PagePool.push_back(page);`

`}`

`return` `page;`

`}`

If there are pages available in the  `m_AvailablePages`  queue, the the  `Page`  at the front of the queue is retrieved an popped off the queue.

If there are no available pages, then a new page is created and pushed to the back the  `m_PagePool`  queue. The  `m_PagePool`  queue stores all of the pages created by the allocator. In this case, the page is not added to the  `m_AvailablePages`  queue because it is going to be used to satisfy the allocation request. When the  `UploadBuffer`  is reset, the  `m_PagePool`  queue is used reset the  `m_AvailablePages`  queue (which is shown later when the  `[Reset](https://www.3dgep.com/learning-directx12-3/#UploadBufferReset)`  function is described).

### UPLOADBUFFER::RESET

The  `Reset`  method is used to reset all of the memory allocations so that they can be reused for the next frame (or more specifically, the next command list recording).

UploadBuffer.cpp

54

55

56

57

58

59

60

61

62

63

64

65

`void UploadBuffer::Reset()`

`{`

`m_CurrentPage = nullptr;`

`// Reset all available pages.`

`m_AvailablePages = m_PagePool;`

`for` `( auto page : m_AvailablePages )`

`{`

`// Reset the page for new allocations.`

`page->Reset();`

`}`

`}`

The  `Reset`  method makes all of the pages available again by copying the  `m_PagePool`to the  **m_AvailablePages**  queue.

On line 60, the available pages are reset to prepare them for new allocations.

The  **UploadBuffer**  can only be reset if all of the allocations made from it are no longer “in-flight” on the command queue. Resetting the  **UploadBuffer**  is controlled by the custom  **CommandList**  class that is shown later.

### UPLOADBUFFER::PAGE::PAGE

The constructor for a  **Page**  takes the size of the page as its only argument.

UploadBuffer.cpp

67

68

69

70

71

72

73

74

75

76

77

78

79

80

81

82

83

84

85

86

`UploadBuffer::Page::Page(``size_t` `sizeInBytes)`

`: m_PageSize(sizeInBytes)`

`, m_Offset(0)`

`, m_CPUPtr(nullptr)`

`, m_GPUPtr(D3D12_GPU_VIRTUAL_ADDRESS(0))`

`{`

`auto device = Application::Get().GetDevice();`

`ThrowIfFailed(device->CreateCommittedResource(`

`&CD3DX12_HEAP_PROPERTIES(D3D12_HEAP_TYPE_UPLOAD),`

`D3D12_HEAP_FLAG_NONE,`

`&CD3DX12_RESOURCE_DESC::Buffer(m_PageSize),`

`D3D12_RESOURCE_STATE_GENERIC_READ,`

`nullptr,`

`IID_PPV_ARGS(&m_d3d12Resource)`

`));`

`m_GPUPtr = m_d3d12Resource->GetGPUVirtualAddress();`

`m_d3d12Resource->Map(0, nullptr, &m_CPUPtr);`

`}`

The  `Page`  constructor also creates the  `[ID3D12Resource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12resource)`  as a committed resource in an upload heap. The creation of committed resource is described in  [Lesson 2](https://www.3dgep.com/learning-directx12-2/#Tutorial2UpdateBufferResource)  and for brevity is not described again here.

After the resource is created, the GPU and CPU addresses are retrieved using the  `[ID3D12Resource::GetGPUVirtualAddress](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12resource-getgpuvirtualaddress)`  and  `[ID3D12Resource::Map](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12resource-map)`  methods respectively. As long as the resource is created in an upload heap, it is safe to leave the resource mapped until the resource is no longer needed.

### UPLOADBUFFER::PAGE::~PAGE

The destructor for the  `Page`  struct unmaps the resource memory using the  `[ID3D12Resource::Unmap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12resource-unmap)`  method and resets the CPU and GPU pointers to 0. Since the  `m_d3d12Resource`  is stored using a  `[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class)`  there is no need to explicitly release it since it will be automatically released after the  `Page`  is destructed.

UploadBuffer.cpp

88

89

90

91

92

93

`UploadBuffer::Page::~Page()`

`{`

`m_d3d12Resource->Unmap(0, nullptr);`

`m_CPUPtr = nullptr;`

`m_GPUPtr = D3D12_GPU_VIRTUAL_ADDRESS(0);`

`}`

Before allocating memory from a  `Page`, the  `Page`  must have enough space to satisfy the allocation request. The  `Page::HasSpace`  method is used to check if the page can satisfy the requested allocation.

### UPLOADBUFFER::PAGE::HASSPACE

The  `Page::HasSpace`  method checks to see if the page can satisfy the requested allocation. This method returns  `true`  if the allocation can be satisfied, or  `false`  if the allocation cannot be satisfied.

UploadBuffer.cpp

95

96

97

98

99

100

101

`bool` `UploadBuffer::Page::HasSpace(``size_t` `sizeInBytes,` `size_t` `alignment )` `const`

`{`

`size_t` `alignedSize = Math::AlignUp(sizeInBytes, alignment);`

`size_t` `alignedOffset = Math::AlignUp(m_Offset, alignment);`

`return` `alignedOffset + alignedSize <= m_PageSize;`

`}`

The  `HasSpace`  method must take the alignment into consideration. If the requested aligned allocation can be satisfied, this method returns  `true`.

### UPLOADBUFFER::PAGE::ALLOCATE

The  `Page::Allocate`  method is where the actual allocation occurs. This method returns an  `Allocation`  structure that can be used to directly copy (using  `[memcpy](http://en.cppreference.com/w/cpp/string/byte/memcpy)`  for example) CPU data to the GPU and bind that GPU address to the pipeline.

UploadBuffer.cpp

103

104

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

120

121

`UploadBuffer::Allocation UploadBuffer::Page::Allocate(``size_t` `sizeInBytes,` `size_t` `alignment)`

`{`

`if` `(!HasSpace(sizeInBytes, alignment))`

`{`

`// Can't allocate space from page.`

`throw` `std::bad_alloc();`

`}`

`size_t` `alignedSize = Math::AlignUp(sizeInBytes, alignment);`

`m_Offset = Math::AlignUp(m_Offset, alignment);`

`Allocation allocation;`

`allocation.CPU =` `static_cast``<``uint8_t``*>(m_CPUPtr) + m_Offset;`

`allocation.GPU = m_GPUPtr + m_Offset;`

`m_Offset += alignedSize;`

`return` `allocation;`

`}`

If the  `Page`  does not have enough space to satisfy the allocation request, this method will throw a  `[std::bad_alloc](http://en.cppreference.com/w/cpp/memory/new/bad_alloc)`  exception.

Since the  [UploadBuffer::Allocate](https://www.3dgep.com/learning-directx12-3/#UploadBufferAllocate)  method already performs a check that the page can satisfy the request, it may be considered redundant to perform the check again in the  `Page::Allocate`  method shown here on lines 105 – 109. Feel free to remove this check in your own implementation.

Both the size and the starting address of an allocation should be aligned to the requested alignment. In most cases the size of the allocation will already be aligned to the requested alignment (for example, when allocating memory for a vertex or index buffer) but to ensure correctness, the requested allocation size is explicitly aligned up to the requested alignment on line 111.

On line 112, the current offset within the page must also be aligned to the requested alignment.

On line 114 – 115 the aligned CPU and GPU addresses are written to the  `Allocation`structure that is returned by this method.

On line 118, the page’s pointer offset is incremented by the aligned size of the allocation.

On line 120, the  `Allocation`  structure is returned to the caller.

You may have noticed that the  `Page::Allocate`  method is not thread safe! If you require thread safety for this method then you may want to insert a  `[std::lock_guard](https://en.cppreference.com/w/cpp/thread/lock_guard)`  before line 105 of this method. Since I do not use the same instance of an  `UploadBuffer`  class across multiple threads, I consider this to be unnecessary overhead (there is some cost associated with locking and unlocking mutexes that I do not want to pay for here).

### UPLOADBUFFER::PAGE::RESET

The  `Page::Reset`  method simply resets the page’s pointer offset to 0 so that it can be used to make new allocations.

UploadBuffer.cpp

123

124

125

126

`void UploadBuffer::Page::Reset()`

`{`

`m_Offset = 0;`

`}`

This concludes the implementation of the  `UploadBuffer`  class. In the next section, the  `DescriptorAllocator`  class is described. As the name implies, the  `DescriptorAllocator`  class is used to allocate (CPU visible) descriptors. CPU visible descriptors are used to create  _views_  for resources (for example  **Render Target Views**(**RTV**),  **Depth-Stencil Views**  (**DSV**),  **Constant Buffer Views**  (**CBV**),  **Shader Resource Views**  (**SRV**),  **Unordered Access Views**  (**UAV**), and  **Samplers**). Before a  **CBV**,  **SRV**,  **UAV**, or  **Sampler**  can be used in a shader, it must be copied to a GPU visible descriptor. The  `DynamicDescriptorHeap`  class handles copying of CPU visible descriptors to GPU visible descriptor heaps. The  `DynamicDescriptorHeap`  class is the subject of the next following sections.

[![Upload Buffer Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for UploadBuffer.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/UploadBuffer.cpp)

# Descriptor Allocator

The  `DescriptorAllocator`  class is used to allocate descriptors from a CPU visible descriptor heap. CPU visible descriptors are useful for “staging” resource descriptors in CPU memory and later copied to a GPU visible descriptor heap for use in a shader.

CPU visible descriptors are used for describing:

-   Render Target Views (RTV)
-   Depth-Stencil Views (DSV)
-   Constant Buffer Views (CBV)
-   Shader Resource Views (SRV)
-   Unordered Access Views (UAV)
-   Samplers

The  `DescriptorAllocator`  class is used to allocate descriptors to the application when loading new resources (like textures). In a typical game engine, resources may need to be loaded and unloaded from memory at sporadic moments while the player moves around the level. To support large dynamic worlds, it may be necessary to initially load some resources, unload them from memory, and reload different resources. The  `DescriptorAllocator`  manages all of the descriptors that are required to describe those resources. Descriptors that are no longer used (for example, when a resource is unloaded from memory) will be automatically returned back to the descriptor heap for reuse.

The  `DescriptorAllocator`  class uses a  _free list_  memory allocation scheme inspired by the  [Variable Sized Memory Allocations Manager](http://diligentgraphics.com/diligent-engine/architecture/d3d12/variable-size-memory-allocations-manager/)  by  [Diligent Graphics](http://diligentgraphics.com/)  [[2]](https://www.3dgep.com/learning-directx12-3/#cite-2)  to manage the descriptors. A  _free list_  keeps track of a list of available allocations. Each entry of the free list stores the available allocations from a page of memory. Each entry of the free list stores the offset from the beginning of the memory page and the size of the available allocation. In order to satisfy the allocation, the free list is searched for an entry that is large enough to satisfy the allocation request. If the allocation cannot be satisfied by the current page, a new page is created in memory.

[![Free List Allocator](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator.png)

The image shows two pages of a free list allocator. The top image shows a memory page with no allocations. In this case, there is only a single entry in the free list which contains the entire page of memory. The bottom image shows the memory page after several allocations have been made.

The above image shows an example of pages of memory that are allocated using a free list allocation strategy. The top image shows the initial state of the page before any allocations are made. In this case, the free list contains only a single entry which refers to the entire memory page. The bottom image shows an example of a memory page after several allocations have been made. In this case, the free list contains several entries which represent the available blocks of memory in the page.

To make a new allocation from the page, all of the entries in the free list are searched and the first block that is large enough to satisfy the request is used. If there are no free blocks that can satisfy the request, then a new page is allocated.

This strategy for allocating memory is called  _first-fit_  (find the first free block that fits) and is the easiest strategy to implement since it only consists of a linear search through the free list but it is not the most efficient method to use for allocation. A linear search has  O(n)O(n)  (worst case) complexity (where  nn  is the number of entries in the free list).

A better technique would be to sort the free blocks by their size and perform a binary-search through the sizes to find a block that is large enough to satisfy the request. If you remember for your algorithm analysis class, a binary search has  O(log2n)O(log2n)  complexity (where  nn  is the number of values to search) which is better than  O(n)O(n).

[![Free List by Size](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator-2.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator-2.png)

The image shows an example of a memory page after several allocations using a free list allocation strategy. The binary tree represents the entries of the free list sorted by size.

The above image shows a memory page after several allocations have been made. The binary tree in the bottom of the image represents the entries of the free list sorted by size. Using the binary tree, an allocation of 160 bytes can be satisfied by searching just three nodes. Using the linear list would require five entries to be searched before the allocation could be satisfied. With only six entries in the free list, this may not seem like a significant performance improvement, but with thousands (or millions) of entries, the performance improvement is significant.

Three different classes are used to implement this strategy:

1.  `DescriptorAllocator`: This is the main interface to the application for requesting descriptors. The  `DescriptorAllocator`  class manages the descriptor pages.
2.  `DescriptorAllocatorPage`: This class is a wrapper for a  `[ID3D12DescriptorHeap](https://msdn.microsoft.com/en-us/library/dn788648(v=vs.85).aspx)`. The  `DescriptorAllocatorPage`  also keeps track of the free list for the page.
3.  `DescriptorAllocation`: This class wraps an allocation that is returned from the  `DescriptorAllocator::Allocate`  method. The  `DescriptorAllocation`  class also stores a pointer back to the page it came from and will automatically free itself if the descriptor(s) are no longer required.

The  `DescriptorAllocator`  class is described first.

## DescriptorAllocator Class

The implementation of the  `DescriptorAllocator`  class is very similar to the  `UploadBuffer`  class shown in the previous section. The  `DescriptorAllocator`  class stores a pool of  `DescriptorAllocatorPage`s. If there are no pages that can satisfy a request, a new page is created and added to the pool. Similar to the  `UploadBuffer`class, the  `DescriptorAllocator`  class has a very simple public interface and only provides a method to allocate descriptors.

### DESCRIPTORALLOCATOR HEADER

The header file for the  `DescriptorAllocator`  class declares the public and private members of the class. The preamble for the header file is shown first which includes the dependencies for the class.

DescriptorAllocator.h

40

41

42

43

44

45

46

47

48

49

50

`#include "DescriptorAllocation.h"`

`#include "d3dx12.h"`

`#include <cstdint>`

`#include <mutex>`

`#include <memory>`

`#include <set>`

`#include <vector>`

`class` `DescriptorAllocatorPage;`

The  `DescriptorAllocator::Allocate`  method returns a  `DescriptorAllocation`  by value which requires the  `DescriptorAllocation.h`  header file to be included (on line 40) in this file.

In order to improve compilation speed, you should try to minimize header file dependencies without introducing external prerequisites (header files should be self-sufficient and not require additional header files to be included first in order to compile). If a dependency can be forward-declared then that should be prefered over including the header file.

The ubiquitous  `d3dx12.h`  header file included on line 42 is required for the DirectX 12 API and helper structures and functions.

The  `[cstdint](http://en.cppreference.com/w/cpp/header/cstdint)`  header file included on line 44 is required for the fixed-width integer types (`uint32_t`, and  `uint64_t`).

The  `[mutex](http://en.cppreference.com/w/cpp/header/mutex)`  header file is included for the  `[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)`  synchronization primitive. The  `[mutex](http://en.cppreference.com/w/cpp/thread/mutex)`  is used in the  `Allocate`  method to allow allocations to be safely made across multiple threads.

The  `[memory](http://en.cppreference.com/w/cpp/header/memory)`  header file is required for the  `[std::shared_ptr](http://en.cppreference.com/w/cpp/memory/shared_ptr)`  pointer class. Shared pointers are used to track the lifetime of the pages. Each allocation also stores a shared pointer back to the page it came from.

The  `[set](http://en.cppreference.com/w/cpp/header/set)`  header file includes the  `[std::set](http://en.cppreference.com/w/cpp/container/set)`  container class. A  `[set](http://en.cppreference.com/w/cpp/container/set)`  is used to store an ordered list of indices to the available pages in the page pool.

The  `[vector](http://en.cppreference.com/w/cpp/header/vector)`  header file includes the  `[std::vector](https://en.cppreference.com/w/cpp/container/vector)`  container class.

The  `DescriptorAllocatorPage`  class is used by the  `DescriptorAllocator`  class but the header file does not need to be included since the  `DescriptorAllocatorPage`  class is only used as a pointer within the  `DescriptorAllocator`  class. In this case, it is sufficient to provide a forward-declaration of the class (on line 50) without the need to include the header file.

The  `DescriptorAllocator`  class defines two public member functions:

1.  `DescriptorAllocator::Allocate`: Allocates a number of contiguous descriptors from a CPU visible descriptor heap.
2.  `DescriptorAllocator::ReleaseStaleDescriptors`: Frees any stale descriptors that can be returned to the list of available descriptors for reuse. This method should only be called after any of the descriptors that were freed are no longer being referenced by the command queue.

The definition of these methods is shown later. The declaration of these methods is made in the header file for the  `DescriptorAllocator`  class.

DescriptorAllocator.h

52

53

54

55

56

57

58

59

60

61

62

63

64

65

66

67

68

69

`class` `DescriptorAllocator`

`{`

`public``:`

`DescriptorAllocator(D3D12_DESCRIPTOR_HEAP_TYPE type,` `uint32_t` `numDescriptorsPerHeap = 256);`

`virtual` `~DescriptorAllocator();`

`/**`

`* Allocate a number of contiguous descriptors from a CPU visible descriptor heap.`

`*`

`* @param numDescriptors The number of contiguous descriptors to allocate.`

`* Cannot be more than the number of descriptors per descriptor heap.`

`*/`

`DescriptorAllocation Allocate(``uint32_t` `numDescriptors = 1);`

`/**`

`* When the frame has completed, the stale descriptors can be released.`

`*/`

`void ReleaseStaleDescriptors( uint64_t frameNumber );`

The  `DescriptorAllocator`  constructor declared on line 55 takes two parameters. The first is the type of descriptors that the  `DescriptorAllocator`  will allocate. This can be one of the  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`,  `[SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`,  `[RTV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`, or  `[DSV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  types.

The second parameter to the constructor is the number of descriptors per descriptor heap. By default, descriptor heaps will be created with 256 descriptors. This value is arbitrary and only needs to be as large as the maximum number of contiguous descriptors that will ever be needed. If all of the descriptors in a descriptor heap have been exhausted, a new heap will be created to satisfy the allocation request.

The  `DescriptorAllocator::Allocate`  method allocates a number contiguous descriptors from a descriptor heap. By default, only a single descriptor is allocated. The  `numDescriptors`  argument can be specified if more than one descriptor is required. This method returns a  `DescriptorAllocation`  which is a wrapper for the allocated descriptor. The  `DescriptorAllocation`  class is described later.

DescriptorAllocator.h

71

72

73

74

75

76

77

78

79

80

81

82

83

84

85

`private``:`

`using` `DescriptorHeapPool = std::vector< std::shared_ptr<DescriptorAllocatorPage> >;`

`// Create a new heap with a specific number of descriptors.`

`std::shared_ptr<DescriptorAllocatorPage> CreateAllocatorPage();`

`D3D12_DESCRIPTOR_HEAP_TYPE m_HeapType;`

`uint32_t` `m_NumDescriptorsPerHeap;`

`DescriptorHeapPool m_HeapPool;`

`// Indices of available heaps in the heap pool.`

`std::set<``size_t``> m_AvailableHeaps;`

`std::mutex m_AllocationMutex;`

`};`

The  `DescriptorHeapPool`  defined on line 72 is a type alias of a  `[std::vector](https://en.cppreference.com/w/cpp/container/vector)`  of  `DescriptorAllocatorPage`s.

The  `DescriptorAllocator::CreateAllocatorPage`  method declared on line 75 is an internal method that is used to create a new allocator page if there are no pages in the page pool that can satisfy the allocation request.

The  `m_HeapType`  variable stores the type of descriptors to allocate. This variable is also used to create new descriptor heaps.

The  `m_NumDescriptorsPerHeap`  variable stores the number of descriptors to create per descriptor heap.

The  `m_HeapPool`  is a  `[std::vector](https://en.cppreference.com/w/cpp/container/vector)`  of  `DescriptorAllocatorPage`s. This variable is used to keep track of all allocated pages.

The  `m_AvailableHeaps`  is a  `[std::set](https://en.cppreference.com/w/cpp/container/set)`  of indices of available pages in the  `m_HeapPool`vector. If all of the descriptors in a  `DescriptorAllocatorPage`  have been exhausted, then the index of that page in the  `m_HeapPool`  vector is removed from the  `m_AvailableHeaps`  set. This ensures that empty pages are skipped when looking for a  `DescriptorAllocatorPage`  that can satisfy the allocation request.

Since the  `DescriptorAllocator`  class is intended to be thread safe, a  `[std::mutex](https://en.cppreference.com/w/cpp/thread/mutex)`  is used to guard against multiple threads allocating or deallocating from the  `DescriptorAllocator`  at the same time.

In the next sections, the implementation of the  `DescriptorAllocator`  is shown.

[![Descriptor Allocator Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocator.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/DescriptorAllocator.h)

### DESCRIPTORALLOCATOR PREAMBLE

Before defining the methods of the  `DescriptorAllocator`  class, a few header files used by the class need to be included.

DescriptorAllocator.cpp

1

2

3

4

`#include <DX12LibPCH.h>`

`#include <DescriptorAllocator.h>`

`#include <DescriptorAllocatorPage.h>`

The  `DX12LibPCH.h`  is the precompiled header file for the  `DX12Lib`  project.

The  `DescriptorAllocator.h`  header file included on line 3 was just described in the previous section and the  `DescriptorAllocatorPage.h`  header file contains the declaration of the  `DescriptorAllocatorPage`  class (which will be shown later).

### DESCRIPTORALLOCATOR::DESCRIPTORALLOCATOR

Similar to the constructor for the  `UploadBuffer`  class shown previously, the constructor for the  `DescriptorAllocator`  class does very little except initializing the class’s member variables.

DescriptorAllocator.cpp

8

9

10

11

12

`DescriptorAllocator::DescriptorAllocator(D3D12_DESCRIPTOR_HEAP_TYPE type,` `uint32_t` `numDescriptorsPerHeap)`

`: m_HeapType(type)`

`, m_NumDescriptorsPerHeap(numDescriptorsPerHeap)`

`{`

`}`

The  `m_HeapType`  and  `m_NumDescriptorsPerHeap`  member variables are initialized based on the arguments passed to the constructor.

### DESCRIPTORALLOCATOR::CREATEALLOCATORPAGE

The  `CreateAllocatorPage`  method is used to create a new page of descriptors. The  `DescriptorAllocatorPage`  class (which will be shown later) is a wrapper for the  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  and manages the actual descriptors.

DescriptorAllocator.cpp

15

16

17

18

19

20

21

22

23

`std::shared_ptr<DescriptorAllocatorPage> DescriptorAllocator::CreateAllocatorPage()`

`{`

`auto newPage = std::make_shared<DescriptorAllocatorPage>( m_HeapType, m_NumDescriptorsPerHeap );`

`m_HeapPool.emplace_back( newPage );`

`m_AvailableHeaps.insert( m_HeapPool.size() - 1 );`

`return` `newPage;`

`}`

The  `DescriptorAllocator::CreateAllocatorPage`  is very simple. On line 17 a new  `DescriptorAllocatorPage`  is created and added to the pool. On line 20, the index of the page in the pool is added to the  `m_AvailableHeaps`  set.

On line 22, the new page is returned to the calling function.

### DESCRIPTORALLOCATOR::ALLOCATE

The  `Allocate`  method allocates a contiguous block of descriptors from a descriptor heap. The method iterates through the available descriptor heap (pages) and tries to allocate the requested number of descriptors until a descriptor heap (page) is able to fulfill the requested allocation. If there are no descriptor heaps that can fulfill the request, then a new descriptor heap (page) is created that can fulfill the request.

DescriptorAllocator.cpp

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

`DescriptorAllocation DescriptorAllocator::Allocate(``uint32_t` `numDescriptors)`

`{`

`std::lock_guard<std::mutex> lock( m_AllocationMutex );`

`DescriptorAllocation allocation;`

`for` `( auto iter = m_AvailableHeaps.begin(); iter != m_AvailableHeaps.end(); ++iter )`

`{`

`auto allocatorPage = m_HeapPool[*iter];`

`allocation = allocatorPage->Allocate( numDescriptors );`

`if` `( allocatorPage->NumFreeHandles() == 0 )`

`{`

`iter = m_AvailableHeaps.erase( iter );`

`}`

`// A valid allocation has been found.`

`if` `( !allocation.IsNull() )`

`{`

`break``;`

`}`

`}`

Before allocating any descriptors, the  `m_AllocationMutex`  mutex is locked to ensure the current thread has exclusive access to the allocator.

The result of the allocation is stored in the  `allocation`  variable defined on line 29.

On lines 31-47, the available descriptor heaps are iterated and on line 35 an allocation of the requested number of descriptors is made. If the allocator page was able to satisfy the requested number of descriptors, then a valid descriptor allocation is returned. If the allocation resulted in the allocator page becoming empty (the number of free descriptor handles reaches 0) then the index of the current page is removed from the set of available heaps (on line 39).

If a valid descriptor handle was allocated from the allocator page (the descriptor handle is not null) then the loop breaks on line 45.

If there were no available allocator pages (which is the case when the  `DescriptorAllocator`  is created) or none of the available allocator pages could satisfy the request, then a new allocator page is created.

DescriptorAllocator.cpp

49

50

51

52

53

54

55

56

57

58

59

`// No available heap could satisfy the requested number of descriptors.`

`if` `( allocation.IsNull() )`

`{`

`m_NumDescriptorsPerHeap = std::max( m_NumDescriptorsPerHeap, numDescriptors );`

`auto newPage = CreateAllocatorPage();`

`allocation = newPage->Allocate( numDescriptors );`

`}`

`return` `allocation;`

`}`

On line 50, the descriptor allocation is checked for validity. If it is still an invalid descriptor (a null descriptor) then a new descriptor page, that is at least as large as the number of requested descriptors, is created on line 53 using the  `[DescriptorAllocator::CreateAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorCreateAllocatorPage)`  method described earlier.

On line 55, the requested allocation is made (which should be guaranteed to succeed) and the resulting allocation is returned to the caller on line 58.

### DESCRIPTORALLOCATOR::RELEASESTALEDESCRIPTORS

The last method of the  `DescriptorAllocator`  class is the  `ReleaseStaleDescriptors`method. The  `ReleaseStaleDescriptors`  method iterates over all of the descriptor heap pages and calls the page’s  `ReleaseStaleDescriptors`  method. If, after releasing the stale descriptors, the page has free handles, it’s added to the list of available heaps.

DescriptorAllocator.cpp

61

62

63

64

65

66

67

68

69

70

71

72

73

74

75

76

`void DescriptorAllocator::ReleaseStaleDescriptors( uint64_t frameNumber )`

`{`

`std::lock_guard<std::mutex> lock( m_AllocationMutex );`

`for` `(` `size_t` `i = 0; i < m_HeapPool.size(); ++i )`

`{`

`auto page = m_HeapPool[i];`

`page->ReleaseStaleDescriptors( frameNumber );`

`if` `( page->NumFreeHandles() > 0 )`

`{`

`m_AvailableHeaps.insert( i );`

`}`

`}`

`}`

In order to prevent modifications of the  `DescriptorAllocator`  in other threads, the  `m_AllocationMutex`  mutex is locked on line 63.

On lines 65-75, the pages of heap pool are iterated calling the page’s  `ReleaseStaleDescriptors`  method. The implementation of the  `DescriptorAllocatorPage::ReleaseStaleDescriptors`  method is shown in the following sections.

Pages that have free descriptor handles are added to the set of available heaps on line 73. It’s okay to add the same index to the set multiple times since the  `[std::set](https://en.cppreference.com/w/cpp/container/set)`  is guaranteed to only store unique values.

[![Descriptor Allocator Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocator.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/DescriptorAllocator.cpp)

## DescriptorAllocatorPage Class

The purpose of the  `DescriptorAllocatorPage`  class is to provide the free list allocator strategy for an  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`. The  `DescriptorAllocatorPage`  class is not intended to be used outside of the  `DescriptorAllocator`  class so the library end user doesn’t necessarily need to know the details of this class. Knowing the details of this class is more interesting to someone who is writing their own DirectX 12 library or to someone who wants to understand the implementation details provided by the  [DX12Lib](https://github.com/jpvanoosten/LearningDirectX12)project that has been created for the purpose of these tutorials. As previously mentioned, the implementation of this class is heavily inspired by  [Variable Size Memory Allocations Manager](http://diligentgraphics.com/diligent-engine/architecture/d3d12/variable-size-memory-allocations-manager/)  from  [Diligent Graphics](http://diligentgraphics.com/)  [[2]](https://www.3dgep.com/learning-directx12-3/#cite-2).

The  `DescriptorAllocatorPage`  class must be able to satisfy descriptor allocation requests but it also needs to provide some functions to query the number of free handles and to check to see if it has sufficient space to satisfy a request. The  `DescriptorAllocatorPage`  provides the following (public) methods:

-   `HasSpace`: Check to see if the  `DescriptorAllocatorPage`  has a contiguous block of descriptors that is large enough to satisfy a request.
-   `NumFreeHandles`: Returns the number of available descriptor handles in the descriptor heap. Note that due to fragmentation of the free list, allocations that are less than or equal to the number of free handles could still fail.
-   `Allocate`: Allocates a number of contiguous descriptors from the descriptor heap. If the  `DescriptorAllocatorPage`  is not able to satisfy the request, this function will return a null  `DescriptorAllocation`
-   `Free`: Returns a  `DescriptorAllocation`  back to the heap. Since descriptors can’t be reused until the command list that is referencing them has finished executing on the command queue, the descriptors are not returned directly to the heap until the render frame has finished executing.
-   `ReleaseStaleDescriptors`: Returns any free’d descriptors back to the descriptor heap for reuse.

### DESCRIPTORALLOCATORPAGE HEADER

The declaration of the  `DescriptorAllocatorPage`  class is slightly more elaborate than the  `[DescriptorAllocator](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocator_Class)`  class described in the previous section. The  `DescriptorAllocatorPage`  class is not only a wrapper for a  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  but also implements a  _free list_  allocator to manage the descriptors in the heap.

DescriptorAllocatorPage.h

37

38

39

40

41

42

43

44

45

46

`#include "DescriptorAllocation.h"`

`#include <d3d12.h>`

`#include <wrl.h>`

`#include <map>`

`#include <memory>`

`#include <mutex>`

`#include <queue>`

Since the  `DescriptorAllocatorPage::Allocate`  method (shown later) returns a  `DescriptorAllocation`  object by value, the header file for  `DescriptorAllocation`  class needs to be included on line 37 (a forward declaration is not sufficient).

The  `d3d12.h`  header file is required for the  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`.

The  `wrl.h`  header file included on line 41 is required for the  `[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class)`  template class.

The  `[map](https://en.cppreference.com/w/cpp/header/map)`,  `[memory](https://en.cppreference.com/w/cpp/header/memory)`,  `[mutex](https://en.cppreference.com/w/cpp/header/mutex)`, and  `[queue](https://en.cppreference.com/w/cpp/header/queue)`  headers are required for the STL types that are used by the  `DescriptorAllocatorPage`  class.

DescriptorAllocatorPage.h

48

49

50

51

52

53

54

55

56

57

58

59

`class` `DescriptorAllocatorPage :` `public` `std::enable_shared_from_this<DescriptorAllocatorPage>`

`{`

`public``:`

`DescriptorAllocatorPage( D3D12_DESCRIPTOR_HEAP_TYPE type,` `uint32_t` `numDescriptors );`

`D3D12_DESCRIPTOR_HEAP_TYPE GetHeapType()` `const``;`

`/**`

`* Check to see if this descriptor page has a contiguous block of descriptors`

`* large enough to satisfy the request.`

`*/`

`bool` `HasSpace(` `uint32_t` `numDescriptors )` `const``;`

The  `DescriptorAllocatorPage`  class publically inherits from the  `[std::enable_shared_from_this](https://en.cppreference.com/w/cpp/memory/enable_shared_from_this)`  template class. The  `[std::enable_shared_from_this](https://en.cppreference.com/w/cpp/memory/enable_shared_from_this)`template class provides the  `[shared_from_this](https://en.cppreference.com/w/cpp/memory/enable_shared_from_this/shared_from_this)`  member function which enables the  `DescriptorAllocatorPage`  class to retrieve a  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)`  from itself (which will be used in the  `DescriptorAllocatorPage::Allocate`  method shown later). This requires the  `DescriptorAllocatorPage`  class to be created from a shared pointer using either  `[std::make_shared](https://en.cppreference.com/w/cpp/memory/shared_ptr/make_shared)`  or  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)<T>( new T(...) )`. This requirement is acceptable in this case since the  `DescriptorAllocatorPage`  class should only be used by the  `DescriptorAllocator`  class. On line 17 of the  `[DescriptorAllocator::CreateAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorCreateAllocatorPage)`  method shown previously, the  `DescriptorAllocatorPage`  is created using the  `[std::make_shared](https://en.cppreference.com/w/cpp/memory/shared_ptr/make_shared)`  method.

The parameterized constructor for the  `DescriptorAllocatorPage`  class is declared on line 51. The constructor takes two arguments: the type of descriptor heap to create and the number of descriptors to allocate in the descriptor heap.

The  `GetHeapType`method declared on line 53 simply returns the descriptor heap type that was used to construct the  `DescriptorAllocatorPage`.

The  `HasSpace`  method declared on line 59 is used to check if the  `DescriptorAllocatorPage`  has a contiguous block of descriptors in the descriptor heap that is large enough to satisfy a request. It is often more efficient to first check if an allocation request will succeed first before making an allocation request and then checking for failure.

DescriptorAllocatorPage.h

61

62

63

64

65

66

67

68

69

70

71

`/**`

`* Get the number of available handles in the heap.`

`*/`

`uint32_t` `NumFreeHandles()` `const``;`

`/**`

`* Allocate a number of descriptors from this descriptor heap.`

`* If the allocation cannot be satisfied, then a NULL descriptor`

`* is returned.`

`*/`

`DescriptorAllocation Allocate(` `uint32_t` `numDescriptors );`

The  `NumFreeHandles`  method defined on line 64 checks how many descriptor handles the  `DescriptorAllocatorPage`  still has available. Due to fragmentation of the free list, an allocation request of a contiguous block of descriptors that is less than the total number of free handles could still fail. For example, the fragmented free list shown in the  [previous image](https://www.3dgep.com/learning-directx12-3/#attachment_8573)  has 544 free descriptors but the largest contiguous block is only 128 descriptors wide.

The  `Allocate`  method defined on line 71 is used to allocate a number of descriptors from the descriptor heap. If the allocation fails, this method returns a null descriptor. This method returns a  `DescriptorAllocation`. To check if the descriptor is valid, the  `DescriptorAllocation::IsNull`  method is used. This method is shown later in the section about the  `DescriptorAllocation`  class.

DescriptorAllocatorPage.h

73

74

75

76

77

78

79

80

81

82

83

84

`/**`

`* Return a descriptor back to the heap.`

`* @param frameNumber Stale descriptors are not freed directly, but put`

`* on a stale allocations queue. Stale allocations are returned to the heap`

`* using the DescriptorAllocatorPage::ReleaseStaleAllocations method.`

`*/`

`void Free( DescriptorAllocation&& descriptorHandle, uint64_t frameNumber );`

`/**`

`* Returned the stale descriptors back to the descriptor heap.`

`*/`

`void ReleaseStaleDescriptors( uint64_t frameNumber );`

The  `Free`  method declared on line 79 is used to free a  `DescriptorAllocation`  that was previously allocated using the  `DescriptorAllocatorPage::Allocate`  method. It is not required to call this method directly since the  `DescriptorAllocation`  class will automatically free itself back to the  `DescriptorAllocatorPage`  it came from if it is no longer in use. This method takes the  `DescriptorAllocation`  as an  [r-value reference](https://en.cppreference.com/w/cpp/language/reference)which implies that the  `DescriptorAllocation`  is moved into the function leaving the original  `DescriptorAllocation`  invalid.

The  `ReleaseStaleDescriptors`  method defined on line 84 releases the stale descriptors back to the descriptor heap for reuse. This method take the  _completed_  frame number as its only argument. All of the descriptors that were released during that frame will be returned to the heap.

The  `DescriptorAllocatorPage`  defines a few additional methods that are internal to this class.

DescriptorAllocatorPage.h

86

87

88

89

90

91

92

93

94

95

96

97

`protected``:`

`// Compute the offset of the descriptor handle from the start of the heap.`

`uint32_t` `ComputeOffset( D3D12_CPU_DESCRIPTOR_HANDLE handle );`

`// Adds a new block to the free list.`

`void AddNewBlock(` `uint32_t` `offset,` `uint32_t` `numDescriptors );`

`// Free a block of descriptors.`

`// This will also merge free blocks in the free list to form larger blocks`

`// that can be reused.`

`void FreeBlock(` `uint32_t` `offset,` `uint32_t` `numDescriptors );`

The  `ComputeOffset`  method computes the number of descriptors from the base descriptor to the specified descriptor handle. This method is used to determine where a descriptor needs to be placed back in heap when the descriptor is free’d.

The  `AddNewBlock`  method adds a block of descriptors to the free list. This method is used to initialize the free list (with a single block containing all descriptors), when splitting a block of descriptors during allocation, and for merging neighboring blocks when descriptors are free’d.

The  `FreeBlock`  method is used to free a block of descriptors. This method is used by the  `ReleaseStaleDescriptors`  method to commit the stale descriptors back to the descriptor heap. The  `FreeBlock`  method also checks if neighboring blocks in the free list can be merged. Merging free blocks in the free list reduces the fragmentation in the free list.

The  `DescriptorAllocatorPage`  class also defines some private data members.

DescriptorAllocatorPage.h

99

100

101

102

103

`private``:`

`// The offset (in descriptors) within the descriptor heap.`

`using` `OffsetType =` `uint32_t``;`

`// The number of descriptors that are available.`

`using` `SizeType =` `uint32_t``;`

In order to improve code readability and reduce ambiguity, the  `OffsetType`  type alias is defined to refer to an offset (in descriptors) within the descriptor heap. The  `SizeType`type alias is defined to refer to the number of descriptors in a block (in the free list).

DescriptorAllocatorPage.h

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

120

121

`struct` `FreeBlockInfo;`

`// A map that lists the free blocks by the offset within the descriptor heap.`

`using` `FreeListByOffset = std::map<OffsetType, FreeBlockInfo>;`

`// A map that lists the free blocks by size.`

`// Needs to be a multimap since multiple blocks can have the same size.`

`using` `FreeListBySize = std::multimap<SizeType, FreeListByOffset::iterator>;`

`struct` `FreeBlockInfo`

`{`

`FreeBlockInfo( SizeType size )`

`: Size( size )`

`{}`

`SizeType Size;`

`FreeListBySize::iterator FreeListBySizeIt;`

`};`

The  `FreeBlockInfo`  struct is forward declared on line 105 and defined on line 113. The forward declaration of the  `FreeBlockInfo`  struct is required to create the  `FreeListByOffset`  type alias on line 107. The  `FreeListByOffset`  type is an alias of a  `[std::map](https://en.cppreference.com/w/cpp/container/map)`  which maps  `FreeBlockInfo`  to the offset of the free block within the free list.

The  `FreeListBySize`  type is an alias of a  `[std::multimap](https://en.cppreference.com/w/cpp/container/multimap)`  that provides a mechanisim to quickly find the first block in the free list that can satisfy an allocation request. The  `FreeListBySize`  type needs to be a  `[std::multimap](https://en.cppreference.com/w/cpp/container/multimap)`  since there can be many blocks in the free list with the same size.

The  `FreeBlockInfo`  struct simply stores the size of the block in the free list and a reference (iterator) to its entry in the  `FreeListBySize`  map. The  `FreeBlockInfo`  struct stores the iterator to its entry in the  `FreeListBySize`  map so that the entry can be quickly removed (without searching) when merging neighboring blocks in the free list.

[![An example of a free list and the corresponding FreeListByOffset and FreeListBySize maps.](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator-1.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Allocator-1.png)

The image shows an example of a free list after several allocations have been made. The  `FreeListByOffset`  data structure (top) stores a reference to the corresponding entry in the  `FreeListBySize`  map (bottom). Similarly, the  `FreeListBySize`  map stores a pointer back to the corresponding entry in the  `FreeListByOffset`  map.

The  [image above](https://www.3dgep.com/learning-directx12-3/#attachment_8710)  shows an example of a free list after several allocations have been made. The  `FreeListByOffset`  data structure stores a reference to the corresponding entry in the  `FreeListBySize`  map. Similarly, each entry in the  `FreeListBySize`  map stores a reference by to the corresponding entry in the  `FreeListByOffset`  map. This solution resembles a bi-directional map ([Bimap in Boost](https://www.boost.org/doc/libs/1_68_0/libs/bimap/doc/html/index.html)) which provides optimized searching on both offset and size of each entry in the free list.

The  `StaleDescriptorInfo`  struct is used to keep track of descriptors in the descriptor heap that have been freed but can’t be reused until the frame in which they were freed is finished executing on the GPU.

DescriptorAllocatorPage.h

123

124

125

126

127

128

129

130

131

132

133

134

135

136

137

`struct` `StaleDescriptorInfo`

`{`

`StaleDescriptorInfo( OffsetType offset, SizeType size, uint64_t frame )`

`: Offset( offset )`

`, Size( size )`

`, FrameNumber( frame )`

`{}`

`// The offset within the descriptor heap.`

`OffsetType Offset;`

`// The number of descriptors`

`SizeType Size;`

`// The frame number that the descriptor was freed.`

`uint64_t FrameNumber;`

`};`

The  `StaleDescriptorInfo`  struct tracks the offset of the first descriptor and the number of descriptors in the descriptor range. The  `FrameNumber`  parameter stores the frame that the descriptors were freed.

DescriptorAllocatorPage.h

139

140

141

142

143

144

145

`// Stale descriptors are queued for release until the frame that they were freed`

`// has completed.`

`using` `StaleDescriptorQueue = std::queue<StaleDescriptorInfo>;`

`FreeListByOffset m_FreeListByOffset;`

`FreeListBySize m_FreeListBySize;`

`StaleDescriptorQueue m_StaleDescriptors;`

The  `StaleDescriptorQueue`  is a type alias for a queue of  `StaleDescriptorInfo`s.

The  `m_FreeListByOffset`,  `m_FreeListBySize`, and  `m_StaleDescriptors`  member variables are the necessary data structures to track the state of the free list.

DescriptorAllocatorPage.h

147

148

149

150

151

152

153

154

155

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> m_d3d12DescriptorHeap;`

`D3D12_DESCRIPTOR_HEAP_TYPE m_HeapType;`

`CD3DX12_CPU_DESCRIPTOR_HANDLE m_BaseDescriptor;`

`uint32_t` `m_DescriptorHandleIncrementSize;`

`uint32_t` `m_NumDescriptorsInHeap;`

`uint32_t` `m_NumFreeHandles;`

`std::mutex m_AllocationMutex;`

`};`

On line 147, the underlying  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  interface is defined.

The  `m_HeapType`  variable defines the type of descriptor heap used by the  `DescriptorAllocatorPage`  class.

Since the increment size of a descriptor within a descriptor heap is vendor specific, it must be queried at runtime (see  [Tutorial 1](https://www.3dgep.com/learning-directx12-1/)  for more information on descriptor heaps). The descriptor increment size is stored in the  `m_DescriptorHandleIncrementSize`member variable.

The total number of descriptor in the descriptor heap is saved in the  `m_NumDescriptorsInHeap`  member variable and the total number of remaining descriptors in the heap is stored in the  `m_NumFreeHandles`  member variable.

The  `m_AllocationMutex`  defined on line 154 is used to ensure safe access allocations and deallocations across multiple threads.

[![Descriptor Allocator Page Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocatorPage.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/DescriptorAllocatorPage.h)

### DESCRIPTORALLOCATORPAGE PREAMBLE

The  `DescriptorAllocatorPage`  class requires a few additional headers in order to compile.

DescriptorAllocatorPage.cpp

1

2

3

4

`#include <DX12LibPCH.h>`

`#include <DescriptorAllocatorPage.h>`

`#include <Application.h>`

The  `DX12LibPCH.h`  provides a precompiled header file for the  `DX12Lib`  project.

The  `DescriptorAllocatorPage.h`  header file is described in the previous section.

The  `Application.h`  header file provides access to the  `Application`  class. The  `Application`  class was briefly described in  [Tutorial 2](https://www.3dgep.com/learning-directx12-2/#DirectX_12_Demo). The  `Application`  class is used to get access to the  `[ID3D12Device](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12device)`  object.

### DESCRIPTORALLOCATORPAGE::DESCRIPTORALLOCATORPAGE

The parameratized constructor for the  `DescriptorAllocatorPage`  class takes the heap type and the number of descriptors to allocate in the heap as arguments.

DescriptorAllocatorPage.cpp

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

`DescriptorAllocatorPage::DescriptorAllocatorPage( D3D12_DESCRIPTOR_HEAP_TYPE type,` `uint32_t` `numDescriptors )`

`: m_HeapType( type )`

`, m_NumDescriptorsInHeap( numDescriptors )`

`{`

`auto device = Application::Get().GetDevice();`

`D3D12_DESCRIPTOR_HEAP_DESC heapDesc = {};`

`heapDesc.Type = m_HeapType;`

`heapDesc.NumDescriptors = m_NumDescriptorsInHeap;`

`ThrowIfFailed( device->CreateDescriptorHeap( &heapDesc, IID_PPV_ARGS( &m_d3d12DescriptorHeap ) ) );`

`m_BaseDescriptor = m_d3d12DescriptorHeap->GetCPUDescriptorHandleForHeapStart();`

`m_DescriptorHandleIncrementSize = device->GetDescriptorHandleIncrementSize( m_HeapType );`

`m_NumFreeHandles = m_NumDescriptorsInHeap;`

`// Initialize the free lists`

`AddNewBlock( 0, m_NumFreeHandles );`

`}`

On line 10, a pointer to the  `[ID3D12Device](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12device)`  is retrieved from the  `Application`  class.

Before creating the  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  object, it must be described. The  `[D3D12_DESCRIPTOR_HEAP_DESC](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_descriptor_heap_desc)`  is used to describe the  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  and has the following members  [[3]](https://www.3dgep.com/learning-directx12-3/#cite-3):

-   `[D3D12_DESCRIPTOR_HEAP_TYPE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type) Type`: Specifies the types of descriptors in the heap.
-   `UINT NumDescriptors`: The number of descriptors in the heap.
-   `[D3D12_DESCRIPTOR_HEAP_FLAGS](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_flags) Flags`: A combination of  `[D3D12_DESCRIPTOR_HEAP_FLAGS](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_flags)`  values that are combined by using a bitwise OR operation. The following flags are currently available:
    -   `D3D12_DESCRIPTOR_HEAP_FLAG_NONE`: Indicates default usage of a heap.
    -   `D3D12_DESCRIPTOR_HEAP_FLAG_SHADER_VISIBLE`: This flag can optionally be set on a descriptor heap to indicate it is be bound on a command list for reference by shaders. Descriptor heaps created without this flag allow applications the option to stage descriptors in CPU memory before copying them to a shader visible descriptor heap, as a convenience. But it is also fine for applications to directly create descriptors into shader visible descriptor heaps with no requirement to stage anything on the CPU.  
        This flag only applies to CBV, SRV, UAV and samplers. It does not apply to other descriptor heap types since shaders do not directly reference the other types.
-   `UINT NodeMask`: For single-adapter operation, set this to zero. If there are multiple adapter nodes, set a bit to identify the node (one of the device’s physical adapters) to which the descriptor heap applies. Each bit in the mask corresponds to a single node. Only one bit must be set.

On line 16, the actual  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`  is created using the  `[ID3D12Device::CreateDescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-createdescriptorheap)`  method.

On line 18, the  `m_BaseDescriptor`  member variable is initialized to the first descriptor handle in the heap and on line 19 the increment size of a descriptor in the descriptor heap is queried using the  `[ID3D12Device::GetDescriptorHandleIncrementSize](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-getdescriptorhandleincrementsize)`  method. On line 20, the number of free handles in the  `DescriptorAllocatorPage`  is initialized to the number of handles in the  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`.

On line 23 a single block of descriptors is added to the free list using the  `AddNewBlock`method. The new block has an offset of 0 and a size of  `m_NumFreeHandles`.

### DESCRIPTORALLOCATORPAGE::GETHEAPTYPE

The  `GetHeapType`  method is simply a  _getter_  method that returns the heap type.

DescriptorAllocatorPage.cpp

26

27

28

29

`D3D12_DESCRIPTOR_HEAP_TYPE DescriptorAllocatorPage::GetHeapType()` `const`

`{`

`return` `m_HeapType;`

`}`

### DESCRIPTORALLOCATORPAGE::NUMFREEHANDLES

The  `NumFreeHandles`  method is simply a getter method that returns the number of free handles that are currently available in the heap.

DescriptorAllocatorPage.cpp

31

32

33

34

`uint32_t` `DescriptorAllocatorPage::NumFreeHandles()` `const`

`{`

`return` `m_NumFreeHandles;`

`}`

### DESCRIPTORALLOCATORPAGE::HASSPACE

The  `HasSpace`  method is used to check if the  `DescriptorAllocatorPage`  has a free block of descriptors that is large enough to satisfy a request for a particular number of descriptors.

DescriptorAllocatorPage.cpp

36

37

38

39

`bool` `DescriptorAllocatorPage::HasSpace(` `uint32_t` `numDescriptors )` `const`

`{`

`return` `m_FreeListBySize.lower_bound(numDescriptors) != m_FreeListBySize.end();`

`}`

The  `[std::map::lower_bound](https://en.cppreference.com/w/cpp/container/map/lower_bound)`  method is used to find the first entry in the free list that is  _not less than_  (in other words:  _greater than or equal to_) the requested number of descriptors. If no such element exists that is  _not less than_  `numDescriptors`, then the  _past-the-end_  iterator is returned which indicates that the free list cannot satisfy the requested number of descriptors. If the  `DescriptorAllocatorPage`  is not able to satisfy the request, then the  `DescriptorAllocator`  will create a new page (as was shown previously in the  `[DescriptorAllocator::Allocate](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorAllocate)`  method).

### DESCRIPTORALLOCATORPAGE::ADDNEWBLOCK

The  `AddNewBlock`  method adds a block to the free list. The block is added to both the  `FreeListByOffset`  map and the  `FreeListBySize`  map. Both lists are linked to create the bi-directional map for optimized lookups.

DescriptorAllocatorPage.cpp

41

42

43

44

45

46

`void DescriptorAllocatorPage::AddNewBlock(` `uint32_t` `offset,` `uint32_t` `numDescriptors )`

`{`

`auto offsetIt = m_FreeListByOffset.emplace( offset, numDescriptors );`

`auto sizeIt = m_FreeListBySize.emplace( numDescriptors, offsetIt.first );`

`offsetIt.first->second.FreeListBySizeIt = sizeIt;`

`}`

On line 43, the  `[std::map::emplace](https://en.cppreference.com/w/cpp/container/map/emplace)`  method is used to emplace an element into the  `m_FreeListByOffset`  map. This method returns a  `[std::pair](https://en.cppreference.com/w/cpp/utility/pair)`  where the first element is an iterator to the inserted element. The iterator to the inserted element is used to add an entry to the  `m_FreeListBySize`  `[multimap](https://en.cppreference.com/w/cpp/container/multimap)`  on line 44.

On line 45, the  `FreeBlockInfo`‘s  `FreeListBySizeIt`  member variable needs to be patched to point to the corresponding iterator in the  `m_FreeListBySize`  `[multimap](https://en.cppreference.com/w/cpp/container/multimap)`.

### DESCRIPTORALLOCATORPAGE::ALLOCATE

The  `Allocate`  method is used to allocate descriptors from the free list. When a block of descriptors is allocated from the free list, it is possible that the existing free block needs to be split and the remaining descriptors are “returned” to the free list. For example, if only a single descriptor is requested by the caller and the free list has a free block of 100 descriptors, then the free block of 100 descriptors is removed from the heap, 1 descriptor allocated from that block, and a free block of 99 descriptors is added back to the free list.

DescriptorAllocatorPage.cpp

48

49

50

`DescriptorAllocation DescriptorAllocatorPage::Allocate(` `uint32_t` `numDescriptors )`

`{`

`std::lock_guard<std::mutex> lock( m_AllocationMutex );`

In order to prevent any race conditions that may occur by multiple threads making allocations on the same  `DescriptorAllocatorPage`, the  `m_AllocationMutex`  is locked line 50.

DescriptorAllocatorPage.cpp

52

53

54

55

56

57

58

59

60

61

62

63

64

65

`// There are less than the requested number of descriptors left in the heap.`

`// Return a NULL descriptor and try another heap.`

`if` `( numDescriptors > m_NumFreeHandles )`

`{`

`return` `DescriptorAllocation();`

`}`

`// Get the first block that is large enough to satisfy the request.`

`auto smallestBlockIt = m_FreeListBySize.lower_bound( numDescriptors );`

`if` `( smallestBlockIt == m_FreeListBySize.end() )`

`{`

`// There was no free block that could satisfy the request.`

`return` `DescriptorAllocation();`

`}`

On lines 54 and 61 the free list is checked to make sure that there are enough free descriptor handles to satisfy the request. If there are not enough descriptor handles, a default (null)  `DescriptorAllocation`  is returned to the calling function. If these checks pass, then  `smallestBlockIt`  contains an iterator to the first entry in the  `FreeListBySize``[multimap](https://en.cppreference.com/w/cpp/container/multimap)`  that is  _not less than_  the requested number of descriptors.

DescriptorAllocatorPage.cpp

67

68

69

70

71

72

73

74

`// The size of the smallest block that satisfies the request.`

`auto blockSize = smallestBlockIt->first;`

`// The pointer to the same entry in the FreeListByOffset map.`

`auto offsetIt = smallestBlockIt->second;`

`// The offset in the descriptor heap.`

`auto offset = offsetIt->first;`

The  `smallestBlockIt`  is used to retrieve the size of the free block and get the iterator to the corresponding entry in the  `FreeListByOffset`  map in  O(1)O(1)  _constant_  time (which is better than  O(log2n)O(log2⁡n)  _logarithmic_  time complexity of the  `[std::map::find](https://en.cppreference.com/w/cpp/container/map/find)`  method).

The free block that was found needs to be removed from the free list and a new block that results from splitting the free block needs to be added back to the free list.

DescriptorAllocatorPage.cpp

76

77

78

79

80

81

82

83

84

85

86

87

88

89

`// Remove the existing free block from the free list.`

`m_FreeListBySize.erase( smallestBlockIt );`

`m_FreeListByOffset.erase( offsetIt );`

`// Compute the new free block that results from splitting this block.`

`auto newOffset = offset + numDescriptors;`

`auto newSize = blockSize - numDescriptors;`

`if` `( newSize > 0 )`

`{`

`// If the allocation didn't exactly match the requested size,`

`// return the left-over to the free list.`

`AddNewBlock( newOffset, newSize );`

`}`

On lines 77-78 the free block that was found is removed from the free list.

On lines 81-82 the size and offset of the the new free block that resulted from splitting the current block is computed and if the size is not 0, the new block is added to the free list using the  `[AddNewBlock](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageAddNewBlock)`  method on line 88.

DescriptorAllocatorPage.cpp

91

92

93

94

95

96

97

`// Decrement free handles.`

`m_NumFreeHandles -= numDescriptors;`

`return` `DescriptorAllocation(`

`CD3DX12_CPU_DESCRIPTOR_HANDLE( m_BaseDescriptor, offset, m_DescriptorHandleIncrementSize ),`

`numDescriptors, m_DescriptorHandleIncrementSize, shared_from_this() );`

`}`

The total number of free handles is decremented by the number of requested descriptors on line 92 and the resulting  `DescriptorAllocation`  is returned to the calling function on line 94.

### DESCRIPTORALLOCATORPAGE::COMPUTEOFFSET

The  `ComputeOffset`  method is used to compute the offset (in descriptor handles) from the base descriptor (first descriptor in the descriptor heap) to a given descriptor.

DescriptorAllocatorPage.cpp

1

2

3

4

`uint32_t` `DescriptorAllocatorPage::ComputeOffset( D3D12_CPU_DESCRIPTOR_HANDLE handle )`

`{`

`return` `static_cast``<``uint32_t``>( handle.ptr - m_BaseDescriptor.ptr ) / m_DescriptorHandleIncrementSize;`

`}`

The  `ComputeOffset`  method is used by the  `Free`  method (shown next) in order to compute the offset of a descriptor in the descriptor heap. Since a  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  is just a structure that contains a single  `SIZE_T`  member variable, computing the offset of a descriptor in a descriptor heap is a matter of simple arithmetic.

### DESCRIPTORALLOCATORPAGE::FREE

The  `Free`  method returns a block of descriptors back to the free list. Descriptors are not immediately returned to the free list but instead are added to a queue of stale descriptors. Descriptors are only returned to the free list once the frame they were freed in is finished executing on the GPU. This ensures that descriptors are not reused until they are no longer being referenced by a GPU command.

DescriptorAllocatorPage.cpp

104

105

106

107

108

109

110

111

112

113

`void DescriptorAllocatorPage::Free( DescriptorAllocation&& descriptor, uint64_t frameNumber )`

`{`

`// Compute the offset of the descriptor within the descriptor heap.`

`auto offset = ComputeOffset( descriptor.GetDescriptorHandle() );`

`std::lock_guard<std::mutex> lock( m_AllocationMutex );`

`// Don't add the block directly to the free list until the frame has completed.`

`m_StaleDescriptors.emplace( offset, descriptor.GetNumHandles(), frameNumber );`

`}`

The  `DescriptorAllocation`  doesn’t store the offset of the descriptor within the descriptor heap but the offset can be computed using the  `ComputeOffset`  method.

In order to guarantee the  `m_StaleDescriptors`  queue is only modified on a single thread at a time, the  `m_AllocationMutex`  `[mutex](https://en.cppreference.com/w/cpp/thread/mutex)`  is locked on line 109 and the  `StaleDescriptorInfo`  is added to the  `m_StaleDescriptors`  queue on line 112.

### DESCRIPTORALLOCATORPAGE::FREEBLOCK

The  `FreeBlock`  method is executed when the stale descriptors are added back to the free list. When adding a block back to the free list, neighboring blocks should be merged to minimize fragmentation of the free list. Two cases need to be considered when adding a block back to the free list:

1.  **Case 1**: There is a block in the free list that is immediately preceding the block being freed.
2.  **Case 2**: There is a block in the free list that is immediately following the block being freed.
3.  **Case 3**: There is both a block in the free list immediately preceding and immediately following the block being freed.
4.  **Case 4**: There is neither a block in the free list immediately preceding nor immediately following the block being freed.

If  **Case 1**  is true then the previous block in the free list needs to be merged with the block being freed. If  **Case 2**  is true then the next block in the free list needs to be merged with the block being freed.

[![](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Merge-1.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Free-List-Merge-1.png)

The previous block in the free list is merged (top). The next block in the free list is merged (bottom). A free block is green, the block being freed is yellow, and an allocated block is red.

The above image shows the two cases that can occur when returning a block back to the free list.  **Case 3**  and  **Case 4**  do not need to be handled in any special way since those cases are already handled implicitly.

DescriptorAllocatorPage.cpp

115

116

117

118

119

120

121

122

123

124

125

126

127

128

129

130

131

132

133

134

135

136

137

138

139

`void DescriptorAllocatorPage::FreeBlock(` `uint32_t` `offset,` `uint32_t` `numDescriptors )`

`{`

`// Find the first element whose offset is greater than the specified offset.`

`// This is the block that should appear after the block that is being freed.`

`auto nextBlockIt = m_FreeListByOffset.upper_bound( offset );`

`// Find the block that appears before the block being freed.`

`auto prevBlockIt = nextBlockIt;`

`// If it's not the first block in the list.`

`if` `( prevBlockIt != m_FreeListByOffset.begin() )`

`{`

`// Go to the previous block in the list.`

`--prevBlockIt;`

`}`

`else`

`{`

`// Otherwise, just set it to the end of the list to indicate that no`

`// block comes before the one being freed.`

`prevBlockIt = m_FreeListByOffset.end();`

`}`

`// Add the number of free handles back to the heap.`

`// This needs to be done before merging any blocks since merging`

`// blocks modifies the numDescriptors variable.`

`m_NumFreeHandles += numDescriptors;`

On line 119, the block that comes after the block being freed is queried from the  `FreeListByOffset`  map using the  `[std::map::upper_bound](https://en.cppreference.com/w/cpp/container/map/upper_bound)`  method. The  `[upper_bound](https://en.cppreference.com/w/cpp/container/map/upper_bound)`method returns the first element whos key is strictly greater than the specified key. If no such element exists, this method returns the  _past-the-end_  (`[end](https://en.cppreference.com/w/cpp/container/map/end)`) iterator.

The previous block in the free list (`prevBlockIt`) is the one that appears just before the block being freed. The previous block is initialized on line 122 to be the same as the next block (`nextBlockIt`) and if it is not the first element in the free list, then it is decremented on line 127 to point to the previous element. If the free list is completely empty (**Case 4**), then the  `nextBlockIt`,  `prevBlockIt`, and  `[begin](https://en.cppreference.com/w/cpp/container/map/begin)`  iterator will all point to the  _past-the-end_  (`[end](https://en.cppreference.com/w/cpp/container/map/end)`) iterator.

If there is only a single item in the free list then it either comes before or after the element being freed. If it comes after the block being freed, then  `nextBlockIt`  will point to that element and  `prevBlockIt`  will be set to the  `[end](https://en.cppreference.com/w/cpp/container/map/end)`  iterator on line 133. If it comes before the block being freed then  `nextBlockIt`  will point to the  `[end](https://en.cppreference.com/w/cpp/container/map/end)`  iterator and the  `prevBlockIt`  will point to that element after being decremented on line 127.

The number of free handles is incremented by the number of handles being freed on line 139.

First  **Case 1**  is checked (the previous block is immediately preceding the block being freed).

DescriptorAllocatorPage.cpp

141

142

143

144

145

146

147

148

149

150

151

152

153

154

155

156

157

158

`if` `( prevBlockIt != m_FreeListByOffset.end() &&`

`offset == prevBlockIt->first + prevBlockIt->second.Size )`

`{`

`// The previous block is exactly behind the block that is to be freed.`

`//`

`// PrevBlock.Offset Offset`

`// | |`

`// |<-----PrevBlock.Size----->|<------Size-------->|`

`//`

`// Increase the block size by the size of merging with the previous block.`

`offset = prevBlockIt->first;`

`numDescriptors += prevBlockIt->second.Size;`

`// Remove the previous block from the free list.`

`m_FreeListBySize.erase( prevBlockIt->second.FreeListBySizeIt );`

`m_FreeListByOffset.erase( prevBlockIt );`

`}`

If there is a block immediately preceding the block being freed then that block is merged with the block being freed.

**Case 2**  is checked next (the next block in the free list is following the block being freed).

DescriptorAllocatorPage.cpp

160

161

162

163

164

165

166

167

168

169

170

171

172

173

174

175

`if` `( nextBlockIt != m_FreeListByOffset.end() &&`

`offset + numDescriptors == nextBlockIt->first )`

`{`

`// The next block is exactly in front of the block that is to be freed.`

`//`

`// Offset NextBlock.Offset`

`// | |`

`// |<------Size-------->|<-----NextBlock.Size----->|`

`// Increase the block size by the size of merging with the next block.`

`numDescriptors += nextBlockIt->second.Size;`

`// Remove the next block from the free list.`

`m_FreeListBySize.erase( nextBlockIt->second.FreeListBySizeIt );`

`m_FreeListByOffset.erase( nextBlockIt );`

`}`

Again, the block immediately following the block being freed is merged with the block being freed.

**Case 3**  and  **Case 4**  do not need to be handled explicitly since they are being implicitly handled.

The final step is to add the new (merged) block back into the free list.

DescriptorAllocatorPage.cpp

177

178

179

`// Add the freed block to the free list.`

`AddNewBlock( offset, numDescriptors );`

`}`

On line 178 the new block is added back into the free list using the  `[AddNewBlock](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageAddNewBlock)`method.

### DESCRIPTORALLOCATORPAGE::RELEASESTALEDESCRIPTORS

Stale descriptors are returned to the free list using the  `ReleaseStaleDescriptors`method when the frame that they were freed in is finished executing on the GPU.

DescriptorAllocatorPage.cpp

179

180

181

182

183

184

185

186

187

188

189

190

191

192

193

194

195

196

`void DescriptorAllocatorPage::ReleaseStaleDescriptors( uint64_t frameNumber )`

`{`

`std::lock_guard<std::mutex> lock( m_AllocationMutex );`

`while` `( !m_StaleDescriptors.empty() && m_StaleDescriptors.front().FrameNumber <= frameNumber )`

`{`

`auto& staleDescriptor = m_StaleDescriptors.front();`

`// The offset of the descriptor in the heap.`

`auto offset = staleDescriptor.Offset;`

`// The number of descriptors that were allocated.`

`auto numDescriptors = staleDescriptor.Size;`

`FreeBlock( offset, numDescriptors );`

`m_StaleDescriptors.pop();`

`}`

`}`

To ensure the  `m_StaleDescriptors`  `[queue](https://en.cppreference.com/w/cpp/container/queue)`  is not being modified on any other thread, the  `m_AllocationMutex`  `[mutex](https://en.cppreference.com/w/cpp/thread/mutex)`  is locked on line 181.

On lines 183-195, the  `m_StaleDescriptors`  `[queue](https://en.cppreference.com/w/cpp/container/queue)`  is checked for any entries. If there is an entry for which the frame number is less than (or equal to) the completed frame number, its entry is popped off the queue and the block is returned back to the free list using the  `[FreeBlock](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageFreeBlock)`  method described in the previous section.

The final class in the triad of classes that constitute the descriptor allocation scheme used by the DX12Lib project is the  `DescriptorAllocation`  class and is the subject of the next section.

[![Descriptor Allocator Page Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocatorPage.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/DescriptorAllocatorPage.cpp)

## DescriptorAllocation Class

The  `DescriptorAllocation`  class is used by the  `DescriptorAllocator`  to represent a single allocation of contiguous descriptors in a descriptor heap. The  `DescriptorAllocation`  class is a move-only self-freeing type that is used as a wrapper for a  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`. The reason why the  `DescriptorAllocation`  must be a move-only class is to ensure there is only a single instance of a particular allocation. This guarantees that if the descriptor is destroyed or replaced, the original descriptor will be returned back to the descriptor heap (from) whence it came.

The  `DescriptorAllocation`  class provides the following (public) method:

-   `IsNull`: Check to see if the  `DescriptorAllocation`  contains a valid descriptor handle.
-   `GetDescriptorHandle`: Get the descriptor handle to the underlying  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`
-   `GetNumHandles`: Gets the number of consecutive descriptors in the  `DescriptorAllocation`.

### DESCRIPTORALLOCATION HEADER

The header file is used to declare the  `DescriptorAllocation`  class. Additional header files that are necessary to compile the  `DescriptorAllocation`  are shown first.

DescriptorAllocation.h

37

38

39

40

41

42

`#include <d3d12.h>`

`#include <cstdint>`

`#include <memory>`

`class` `DescriptorAllocatorPage;`

The  `d3d12.h`  header is necessary for the  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  type.

The  `[cstdint](https://en.cppreference.com/w/cpp/header/cstdint)`  header file is included to provide the  `[uint32_t](https://en.cppreference.com/w/cpp/types/integer)`  type.

The  `[memory](https://en.cppreference.com/w/cpp/header/memory)`  header file is included to provide access to the  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)`  type.

The  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  is forward declared on line 42 to avoid including the header file for that class. The  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  is used as a template argument for a  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)`  which doesn’t require a complete type.

DescriptorAllocation.h

44

45

46

47

48

49

50

51

52

53

`class` `DescriptorAllocation`

`{`

`public``:`

`// Creates a NULL descriptor.`

`DescriptorAllocation();`

`DescriptorAllocation( D3D12_CPU_DESCRIPTOR_HANDLE descriptor,` `uint32_t` `numHandles,` `uint32_t` `descriptorSize, std::shared_ptr<DescriptorAllocatorPage> page );`

`// The destructor will automatically free the allocation.`

`~DescriptorAllocation();`

The  `DescriptorAllocation`  class provides a default constructor which initializes the descriptor as a  _null_  descriptor.

The parameterized constructor declared on line 50 is used by the  `[DescriptorAllocatorPage::Allocate](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageAllocate)`  method to construct a valid  `DescriptorAllocation`.

The destructor declared on line 53 is necessary to ensure the allocation is returned to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  that it came from.

DescriptorAllocation.h

55

56

57

58

59

60

61

`// Copies are not allowed.`

`DescriptorAllocation(` `const` `DescriptorAllocation& ) =` `delete``;`

`DescriptorAllocation& operator=(` `const` `DescriptorAllocation& ) =` `delete``;`

`// Move is allowed.`

`DescriptorAllocation( DescriptorAllocation&& allocation );`

`DescriptorAllocation& operator=( DescriptorAllocation&& other );`

It is not allowed to make copies of the  `DescriptorAllocation`  to prevent any accidental copies, the copy constructor and copy assignment operator are deleted from the class to prevent the compiler from auto generating them.

Moving the  `DescriptorAllocation`  to another  `DescriptorAllocation`  is allowed (and in fact, required). Both the move constructor and the move assignment operator are declared on lines 60 and 61.

DescriptorAllocation.h"

63

64

`// Check if this a valid descriptor.`

`bool` `IsNull()` `const``;`

The  `IsNull`  method is used to check if the  `DescriptorAllocation`  contains a valid descriptor.

DescriptorAllocation.h

66

67

`// Get a descriptor at a particular offset in the allocation.`

`D3D12_CPU_DESCRIPTOR_HANDLE GetDescriptorHandle(` `uint32_t` `offset = 0 )` `const``;`

The  `DescriptorAllocation`  can contain a block of consecutive descriptors in a descriptor heap. The  `GetDescriptorHandle`  method is used to get the underlying  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  at a particular offset within the contigious block of descriptors.

DescriptorAllocation.h

69

70

`// Get the number of (consecutive) handles for this allocation.`

`uint32_t` `GetNumHandles()` `const``;`

The  `GetNumHandles`  is used to get the number of consecutive descriptor handles that are contained in the  `DescriptorAllocation`.

DescriptorAllocation.h

72

73

74

`// Get the heap that this allocation came from.`

`// (For internal use only).`

`std::shared_ptr<DescriptorAllocatorPage> GetDescriptorAllocatorPage()` `const``;`

The  `GetDescriptorAllocatorPage`  method is used to query the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  where the  `DescriptorAllocation`  came from.

DescriptorAllocation.h

76

77

78

79

80

81

82

83

84

85

86

87

88

89

`private``:`

`// Free the descriptor back to the heap it came from.`

`void Free();`

`// The base descriptor.`

`D3D12_CPU_DESCRIPTOR_HANDLE m_Descriptor;`

`// The number of descriptors in this allocation.`

`uint32_t` `m_NumHandles;`

`// The offset to the next descriptor.`

`uint32_t` `m_DescriptorSize;`

`// A pointer back to the original page where this allocation came from.`

`std::shared_ptr<DescriptorAllocatorPage> m_Page;`

`};`

The  `Free`  method is used by the  `DescriptorAllocation`  class to return itself back to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  it came from. This method is used if the  `DescriptorAllocation`  is destructed or when another  `DescriptorAllocation`  is being (move) assigned to it.

The  `m_Descriptor`  member variable is the handle to the first  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  in the allocation.

The  `m_NumHandles`  member variable stores the total number of descriptors in the  `DescriptorAllocation`.

The  `m_DescriptorSize`  member variable stores the increment size for each descriptor. This is used to compute the offset of a particular descriptor within the allocation.

The  `m_Page`  member variable stores a  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)`  back to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  that the  `DescriptorAllocation`  came from.

[![Descriptor Allocation Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocation.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/DescriptorAllocation.h)

### DESCRIPTORALLOCATION PREAMBLE

The implementation of the  `DescriptorAllocation`  class is fairly simple as it acts as a wrapper class for the underlying  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  and provides a few accessor methods that describe the allocation.

DescriptorAllocation.cpp

1

2

3

4

5

6

`#include <DX12LibPCH.h>`

`#include <DescriptorAllocation.h>`

`#include <Application.h>`

`#include <DescriptorAllocatorPage.h>`

The  `DX12LibPCH.h`  header file provides the precompiled header file for the  `DX12Lib`project and must be the first include that appears in the implementation file.

The  `DescriptorAllocation.h`  header is included next and provides the declaration of the  `DescriptorAllocation`  class that was shown in the previous section.

The  `Application.h`  header provides the declaration of the  `Application`  class. When freeing a  `DescriptorAllocation`  it is necessary to provide the current frame of execution which is provided by the  `Application`  class.

The  `DescriptorAllocatorPage.h`  header file is necessary to be able to call the  `[DescriptorAllocatorPage::Free](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageFree)`  method when freeing the  `DescriptorAllocation`.

### DESCRIPTORALLOCATION DEFAULT CONSTRUCTOR

The default constructor for the  `DescriptorAllocation`  class simply initializes it as a  _null_descriptor.

DescriptorAllocation.cpp

8

9

10

11

12

13

`DescriptorAllocation::DescriptorAllocation()`

`: m_Descriptor{ 0 }`

`, m_NumHandles( 0 )`

`, m_DescriptorSize( 0 )`

`, m_Page( nullptr )`

`{}`

### DESCRIPTORALLOCATION PARAMERATIZED CONSTRUCTOR

The parameterized constructor for the  `DescriptorAllocation`  class initializes it as a valid descriptor (assuming the parameters are valid).

DescriptorAllocation.cpp

15

16

17

18

19

20

`DescriptorAllocation::DescriptorAllocation( D3D12_CPU_DESCRIPTOR_HANDLE descriptor,` `uint32_t` `numHandles,` `uint32_t` `descriptorSize, std::shared_ptr<DescriptorAllocatorPage> page )`

`: m_Descriptor( descriptor )`

`, m_NumHandles( numHandles )`

`, m_DescriptorSize( descriptorSize )`

`, m_Page( page )`

`{}`

The member variables being initialized here are described in the  [DescriptorAllocation Header](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocation_Header)  section and shouldn’t require additional explanation.

### DESCRIPTORALLOCATION DESTRUCTOR

The destructor for the  `DescriptorAllocation`  class must ensure that the descriptor is freed back to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  it came from by calling the  `Free`  method.

DescriptorAllocation.cpp

23

24

25

26

`DescriptorAllocation::~DescriptorAllocation()`

`{`

`Free();`

`}`

### DESCRIPTORALLOCATION MOVE CONSTRUCTOR

The move constructor allows the  `DescriptorAllocation`  to be  _moved_. The original  `DescriptorAllocation`  must be made invalid but the allocation should not be  _freed_.

DescriptorAllocation.cpp

28

29

30

31

32

33

34

35

36

37

`DescriptorAllocation::DescriptorAllocation( DescriptorAllocation&& allocation )`

`: m_Descriptor(allocation.m_Descriptor)`

`, m_NumHandles(allocation.m_NumHandles)`

`, m_DescriptorSize(allocation.m_DescriptorSize)`

`, m_Page(std::move(allocation.m_Page))`

`{`

`allocation.m_Descriptor.ptr = 0;`

`allocation.m_NumHandles = 0;`

`allocation.m_DescriptorSize = 0;`

`}`

### DESCRIPTORALLOCATION MOVE ASSIGNMENT

The move assignment operator behaves similar to the move constructor except the original descriptor must be freed using the  `Free`  method before moving another descriptor into the current one.

DescriptorAllocation.cpp

39

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

`DescriptorAllocation& DescriptorAllocation::operator=( DescriptorAllocation&& other )`

`{`

`// Free this descriptor if it points to anything.`

`Free();`

`m_Descriptor = other.m_Descriptor;`

`m_NumHandles = other.m_NumHandles;`

`m_DescriptorSize = other.m_DescriptorSize;`

`m_Page = std::move( other.m_Page );`

`other.m_Descriptor.ptr = 0;`

`other.m_NumHandles = 0;`

`other.m_DescriptorSize = 0;`

`return` `*``this``;`

`}`

### DESCRIPTORALLOCATION::FREE

If the  `DescriptorAllocation`  either goes out of scope or is replaced by another descriptor, it must be freed. The  `Free`  method is used to return the  `DescriptorAllocation`  back to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  it came from.

DescriptorAllocation.cpp

56

57

58

59

60

61

62

63

64

65

66

67

`void DescriptorAllocation::Free()`

`{`

`if` `( !IsNull() && m_Page )`

`{`

`m_Page->Free( std::move( *``this` `), Application::GetFrameCount() );`

`m_Descriptor.ptr = 0;`

`m_NumHandles = 0;`

`m_DescriptorSize = 0;`

`m_Page.reset();`

`}`

`}`

If the  `DescriptorAllocation`  is valid (not  _null_) then it is returned back to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  it came from using the  `[DescriptorAllocatorPage::Free](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPageFree)`method.

### DESCRIPTORALLOCATION::ISNULL

The  `IsNull`  method check to see if the underlying  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  is valid.

DescriptorAllocation.cpp

69

70

71

72

73

`// Check if this a valid descriptor.`

`bool` `DescriptorAllocation::IsNull()` `const`

`{`

`return` `m_Descriptor.ptr == 0;`

`}`

### DESCRIPTORALLOCATION::GETDESCRIPTORHANDLE

The  `GetDescriptorHandle`  method returns a  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  for the descriptor at a particular offset within the  `DescriptorAllocation`.

DescriptorAllocation.cpp

75

76

77

78

79

80

`// Get a descriptor at a particular offset in the allocation.`

`D3D12_CPU_DESCRIPTOR_HANDLE DescriptorAllocation::GetDescriptorHandle(` `uint32_t` `offset )` `const`

`{`

`assert``( offset < m_NumHandles );`

`return` `{ m_Descriptor.ptr + ( m_DescriptorSize * offset ) };`

`}`

### DESCRIPTORALLOCATION::GETNUMHANDLES

The  `GetNumHandles`  method returns the number of descriptor handles in the  `DescriptorAllocation`.

DescriptorAllocation.cpp

82

83

84

85

`uint32_t` `DescriptorAllocation::GetNumHandles()` `const`

`{`

`return` `m_NumHandles;`

`}`

### DESCRIPTORALLOCATION::GETDESCRIPTORALLOCATORPAGE

The  `GetDescriptorAllocatorPage`  method returns the  `[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr)`  to the  `[DescriptorAllocatorPage](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocatorPage_Class)`  where the  `DescriptorAllocation`  originated from.

DescriptorAllocation.cpp

87

88

89

90

`std::shared_ptr<DescriptorAllocatorPage> DescriptorAllocation::GetDescriptorAllocatorPage()` `const`

`{`

`return` `m_Page;`

`}`

This concludes the description of the classes that are used to implement the descriptor allocation strategy used by the DX12Lib project. The  `[DescriptorAllocator](https://www.3dgep.com/learning-directx12-3/#DescriptorAllocator_Class)`  class provides a simple interface for allocating and freeing descriptors using a  _free list_memory management scheme. The  `DescriptorAllocatorPage`  class is used internally to manage allocations and the  `DescriptorAllocation`  class is used to represent a single allocation from the descriptor heap.

The  `DynamicDescriptorHeap`  class provides a flexible solution for ensuring the CPU visible descriptors are copied to the correct location in a GPU visible descriptor heap for rendering on the GPU. The  `DynamicDescriptorHeap`  class is the subject of the next section.

[![Descriptor Allocation Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DescriptorAllocation.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/DescriptorAllocation.cpp)

# Dynamic Descriptor Heap

The purpose of the  `DynamicDescriptorHeap`  class is to allocate GPU visible descriptors that are used for binding CBV, SRV, UAV, and Samplers to the GPU pipeline for rendering or compute invocations. This is necessary since the descriptors provided by the  `DescriptorAllocator`  class shown in the previous section are CPU visible and cannot be used to bind resources to the GPU rendering pipeline. The  `DynamicDescriptorHeap`  class provides a staging area for CPU visible descriptors that are committed to GPU visible descriptor heaps when a  `Draw`  or  `Dispatch`  method is invoked on the command list.

Since only a single  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  descriptor heap and a single  `[SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  descriptor heap can be bound to the command list at the same time, the  `DynamicDescriptorHeap`  class also ensures that the currently bound descriptor heap has a sufficient number of descriptors to commit all of the staged descriptors before a  `Draw`  or  `Dispatch`command is executed. If the currently bound descriptor heap runs out of descriptors, then a new descriptor heap is bound to the command list.

It should be noted that dynamic descriptor indexing and unbounded descriptor arrays were added in Shader Model 5.1. See  [Dynamic Indexing using HLSL 5.1](https://docs.microsoft.com/en-us/windows/desktop/direct3d12/dynamic-indexing-using-hlsl-5-1)  for more information. The  `DynamicDescriptorHeap`  class shown in this article is designed to provide functionality similar to that of DirectX 11 where dynamic descriptor indexing wasn’t supported.  

The  `DynamicDescriptorHeap`  class caches staged descriptors in a descriptor cache that is configured to match the layout of the root signature. For example, if the root signature has the following layout:

INDEX

TYPE

RANGE TYPE

NUM DESRIPTORS

0

CBV

–

–

1

DESCRIPTOR_TABLE

SRV

6

2

DESCRIPTOR_TABLE

CBV

3

3

DESCRIPTOR_TABLE

UAV

3

4

DESCRIPTOR_TABLE

SAMPLER

4

Then the descriptor table cache for the  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  dynamic descriptor heap would look like this:

[![Each entry in the descriptor table cache stores the number descriptors and a pointer to the descriptors in the descriptor handle cache. Descriptors are committed to the corresponding entries in the root signature before a Draw or Dispatch command is executed.](https://www.3dgep.com/wp-content/uploads/2018/06/Dynamic-Descriptor-Heap-1.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Dynamic-Descriptor-Heap-1.png)

The image shows the layout of the  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  descriptor table cache. Each entry in the descriptor table cache stores the number descriptors and a pointer to the descriptors in the descriptor handle cache. Descriptors are committed to the corresponding entries in the root signature before a  `Draw`  or  `Dispatch`  command is executed.

There are a few interesting things to note in the  [image above](https://www.3dgep.com/learning-directx12-3/#attachment_8808). The first entry (root index 0) in the descriptor table cache is empty because the root signature contains an inline  **Constant Buffer View**  (**CBV**). Since an inline  **CBV**  does not require a descriptor, there is no reason to allocate any space for it in the descriptor handle cache.

The second entry in the descriptor table cache has six  **SRV**  descriptors and a pointer to the first entry in the descriptor handle cache. Similarly, the third and fourth entries in the descriptor table cache each have three descriptors and a pointer to their corresponding entry in the descriptor handle cache.

The fourth entry in the descriptor table cache is empty despite the fact that the root signature layout has a descriptor table that contains four  `[SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`s. Since  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`descriptors and  `[SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  descriptors cannot be stored in the same descriptor heap, there is a seperate  `DynamicDescriptorHeap`  for each  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  and  `[SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`descriptor types.

## DynamicDescriptorHeap Class

The design of the  `DynamicDescriptorHeap`  class is heavily based on the  [DynamicDescriptorHeap](https://github.com/Microsoft/DirectX-Graphics-Samples/blob/master/MiniEngine/Core/DynamicDescriptorHeap.h)  implementation from  [Microsoft’s DirectX Samples on GitHub](https://github.com/Microsoft/DirectX-Graphics-Samples)[[1]](https://www.3dgep.com/learning-directx12-3/#cite-1).

The  `DynamicDescriptorHeap`  class provides the following functionality:

-   **Stage Descriptors**: Stage CPU visible descriptors to the descriptor table cache.
-   **Commit Staged Descriptors**: Commit the staged descriptors to a GPU visible descriptor heap.
-   **Copy a Descriptor**: Directly copy a CPU visible descriptor to a GPU visible descriptor heap. This is useful for the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewFloat](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewfloat)`  and the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewUint](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewuint)`  methods.

### DYNAMICDESCRIPTORHEAP HEADER

In this section the declaration of the  `DynamicDescriptorHeap`  class is described. The  `DynamicDescriptorHeap`  class provides methods for staging CPU visible descriptors and committing those descriptors to a GPU visible descriptor heap before a  `Draw`  or  `Dispatch`  command is executed. The  `DynamicDescriptorHeap`  class also provides a method to copy a single CPU visible descriptor to a GPU visible descriptor heap. Copying of single descriptors is required for the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewFloat](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewfloat)`  and the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewUint](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewuint)`  methods. These methods require both a CPU and a GPU visible descriptor for the resource to be cleared.

A method to parse the root signature and configure the descriptor table cache is also provided. The DX12Lib project provides a  `RootSignature`  class for the purpose of determining the layout of the root signature but this class is not described here. The  `RootSignature`  class is a wrapper for a  `[ID3D12RootSignature](https://msdn.microsoft.com/en-us/library/windows/desktop/dn788714(v=vs.85).aspx)`. For more information on the  `RootSignature`  class, refer to the GitHub repository ([RootSignature.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/RootSignature.h), and  [RootSignature.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/RootSignature.cpp)).

DynamicDescriptorHeap.h

1

2

3

4

5

6

7

8

9

10

`#include "d3dx12.h"`

`#include <wrl.h>`

`#include <cstdint>`

`#include <memory>`

`#include <queue>`

`class` `CommandList;`

`class` `RootSignature;`

The  `d3dx12.h`  header file provides some helper types for working with DirectX 12. The  `d3dx12.h`  header file also includes the  `d3d12.h`  file so it does not need to be included directly.

The  `wrl.h`  header file includes the  `[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class?view=vs-2017)`  template class.

The  `[cstdint](https://en.cppreference.com/w/cpp/header/cstdint)`  header provides access to the standard integer types (such as  `uint32_t`). The  `[memory](https://en.cppreference.com/w/cpp/header/memory)`  header file is required for the  `[std::unique_ptr](https://en.cppreference.com/w/cpp/memory/unique_ptr)`  and the  `[queue](https://en.cppreference.com/w/cpp/header/queue)`header file is required for the  `[std::queue](https://en.cppreference.com/w/cpp/container/queue)`  container class.

The  `CommandList`  and  `RootSignature`  classes are forward declared on lines 9 and 10. The header files are only required in the implementation file for the  `DynamicDescriptorHeap`  class.

DynamicDescriptorHeap.h

48

49

50

51

52

53

54

55

`class` `DynamicDescriptorHeap`

`{`

`public``:`

`DynamicDescriptorHeap(`

`D3D12_DESCRIPTOR_HEAP_TYPE heapType,`

`uint32_t` `numDescriptorsPerHeap = 1024);`

`virtual` `~DynamicDescriptorHeap();`

The  `DynamicDescriptorHeap`  class has a single constructor which takes a  `[D3D12_DESCRIPTOR_HEAP_TYPE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  argument and the number of descriptors to allocate per heap.

On line 55, the destructor for the  `DynamicDescriptorHeap`  class is declared.

DynamicDescriptorHeap.h

1

2

3

4

5

6

`/**`

`* Stages a contiguous range of CPU visible descriptors.`

`* Descriptors are not copied to the GPU visible descriptor heap until`

`* the CommitStagedDescriptors function is called.`

`*/`

`void StageDescriptors(``uint32_t` `rootParameterIndex,` `uint32_t` `offset,` `uint32_t` `numDescriptors,` `const` `D3D12_CPU_DESCRIPTOR_HANDLE srcDescriptors);`

CPU visible descriptors are  _staged_  to the  `DynamicDescriptorHeap`  using the  `StageDescriptors`  method. This method has the following arguments:

-   `uint32_t rootParameterIndex`: The index of root parameter to copy the descriptors to. This must be configured as a  `[DESCRIPTOR_TABLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_root_parameter_type)`  in the currently bound root signature.
-   `uint32_t offset`: The offset within the descriptor table to copy the descriptors to. This value can span descriptor ranges within the table but  `offset`  +  `numDescriptors`  must not exceed the total number of descriptors in the descriptor table.
-   `uint32_t numDescriptors`: The number of contiguous descriptors to copy starting from  `srcDescriptors`.
-   `const [D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle) srcDescriptors`: The base descriptor to start copying descriptors from.

The  `StageDescriptors`  method is used to copy any number of contiguous CPU visible descriptors to the  `DynamicDescriptorHeap`. Using this method, only the descriptor handles are copied to the  `DynamicDescriptorHeap`  but not the contents of the descriptor. For this reason, the CPU visible descriptors cannot be reused or overwritten (using  `[ID3D12Device::CreateShaderResourceView](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-createshaderresourceview)`  for example) until the  `CommitStagedDescriptors`  method is invoked.

DynamicDescriptorHeap.h

64

65

66

67

68

69

70

71

72

73

74

75

76

77

`/**`

`* Copy all of the staged descriptors to the GPU visible descriptor heap and`

`* bind the descriptor heap and the descriptor tables to the command list.`

`* The passed-in function object is used to set the GPU visible descriptors`

`* on the command list. Two possible functions are:`

`* * Before a draw : ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable`

`* * Before a dispatch: ID3D12GraphicsCommandList::SetComputeRootDescriptorTable`

`*`

`* Since the DynamicDescriptorHeap can't know which function will be used, it must`

`* be passed as an argument to the function.`

`*/`

`void CommitStagedDescriptors( CommandList& commandList, std::function<void(ID3D12GraphicsCommandList*,` `UINT``, D3D12_GPU_DESCRIPTOR_HANDLE)> setFunc );`

`void CommitStagedDescriptorsForDraw(CommandList& commandList);`

`void CommitStagedDescriptorsForDispatch(CommandList& commandList);`

The  `CommitStagedDescriptors`  family of methods is used to commit any staged descriptors to the GPU visible descriptor heaps. The  `CommitStagedDescriptorsForDraw`uses the  `[ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setgraphicsrootdescriptortable)`  method to bind the descriptors to the graphics pipeline while the  `CommitStagedDescriptorsForDispatch`method uses the  `[ID3D12GraphicsCommandList::SetComputeRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setcomputerootdescriptortable)`  method to bind the descriptors to the compute pipeline.

DynamicDescriptorHeap.h

79

80

81

82

83

84

85

86

87

88

89

90

91

92

93

94

`/**`

`* Copies a single CPU visible descriptor to a GPU visible descriptor heap.`

`* This is useful for the`

`* * ID3D12GraphicsCommandList::ClearUnorderedAccessViewFloat`

`* * ID3D12GraphicsCommandList::ClearUnorderedAccessViewUint`

`* methods which require both a CPU and GPU visible descriptors for a UAV`

`* resource.`

`*`

`* @param commandList The command list is required in case the GPU visible`

`* descriptor heap needs to be updated on the command list.`

`* @param cpuDescriptor The CPU descriptor to copy into a GPU visible`

`* descriptor heap.`

`*`

`* @return The GPU visible descriptor.`

`*/`

`D3D12_GPU_DESCRIPTOR_HANDLE CopyDescriptor( CommandList& comandList, D3D12_CPU_DESCRIPTOR_HANDLE cpuDescriptor);`

When clearing a UAV resources using either the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewFloat](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewfloat)`  or the  `[ID3D12GraphicsCommandList::ClearUnorderedAccessViewUint](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-clearunorderedaccessviewuint)`  method, both a CPU and a GPU visible descriptor are required. The  `CopyDescriptor`  method is used to copy a single CPU visible descriptor into a GPU visible descriptor heap. This method accepts a  `CommandList`  as its only argument in case the currently bound descriptor heap needs to be updated on the command list as a result of copying the descriptor.

DynamicDescriptorHeap.h

96

97

98

99

100

101

`/**`

`* Parse the root signature to determine which root parameters contain`

`* descriptor tables and determine the number of descriptors needed for`

`* each table.`

`*/`

`void ParseRootSignature(` `const` `RootSignature& rootSignature);`

Using the  `ParseRootSignature`  method, the the  `DynamicDescriptorHeap`  is informed of any changes to the currently bound root signature on the command list. This method updates the layout of the descriptors in the descriptor cache to match the descriptor layout in the root signature (as described in the  [introduction to this section](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)).

DynamicDescriptorHeap.h

103

104

105

106

107

108

`/**`

`* Reset used descriptors. This should only be done if any descriptors`

`* that are being referenced by a command list has finished executing on the`

`* command queue.`

`*/`

`void Reset();`

The  `Reset`  method is used to reset the allocated descriptor heaps and descriptor cache. This should only be done when the command queue is finished processing any commands that are referencing any descriptors in the  `DynamicDescriptorHeap`.

DynamicDescriptorHeap.h

112

113

114

115

116

`private``:`

`// Request a descriptor heap if one is available.`

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> RequestDescriptorHeap();`

`// Create a new descriptor heap of no descriptor heap is available.`

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> CreateDescriptorHeap();`

The  `RequestDescriptorHeap`  method is used to get an available descriptor heap. If there are no available descriptor heaps, then a new descriptor heap is created using the  `CreateDescriptorHeap`  method.

DynamicDescriptorHeap.h

118

119

120

`// Compute the number of stale descriptors that need to be copied`

`// to GPU visible descriptor heap.`

`uint32_t` `ComputeStaleDescriptorCount()` `const``;`

The  `ComputeStaleDescriptorCount`  method returns the number of CPU visible descriptors that need to be copied to the GPU visible descriptor heap.

DynamicDescriptorHeap.h

122

123

124

125

126

127

`/**`

`* The maximum number of descriptor tables per root signature.`

`* A 32-bit mask is used to keep track of the root parameter indices that`

`* are descriptor tables.`

`*/`

`static` `const` `uint32_t` `MaxDescriptorTables = 32;`

The  `MaxDescriptorTables`  constant represents the maximum number of descriptor tables that can exist in the root signature. The limit of 32 descriptor tables was chosen since a 32-bit bitmask is used to indicate which entries of the root signature uses a descriptor table.

DynamicDescriptorHeap.h

129

130

131

132

133

134

135

136

137

138

139

140

141

142

143

144

145

146

147

148

149

150

`/**`

`* A structure that represents a descriptor table entry in the root signature.`

`*/`

`struct` `DescriptorTableCache`

`{`

`DescriptorTableCache()`

`: NumDescriptors(0)`

`, BaseDescriptor(nullptr)`

`{}`

`// Reset the table cache.`

`void Reset()`

`{`

`NumDescriptors = 0;`

`BaseDescriptor = nullptr;`

`}`

`// The number of descriptors in this descriptor table.`

`uint32_t` `NumDescriptors;`

`// The pointer to the descriptor in the descriptor handle cache.`

`D3D12_CPU_DESCRIPTOR_HANDLE* BaseDescriptor;`

`};`

The  `DescriptorTableCache`  struct represents a single entry in the  `DescriptorTableCache`  array. Each entry in the descriptor cache stores the number of descriptors in the descriptor table and a pointer to the descriptor handle in the descriptor handle cache. By default, each entry in the descriptor table cache is empty (0 descriptors and a null pointer) which indicates that that entry in the currently bound root signature does not use a descriptor table.

DynamicDescriptorHeap.h

152

153

154

155

156

157

158

159

160

161

162

163

164

165

`// Describes the type of descriptors that can be staged using this`

`// dynamic descriptor heap.`

`// Valid values are:`

`// * D3D12_DESCRIPTOR_HEAP_TYPE_CBV_SRV_UAV`

`// * D3D12_DESCRIPTOR_HEAP_TYPE_SAMPLER`

`// This parameter also determines the type of GPU visible descriptor heap to`

`// create.`

`D3D12_DESCRIPTOR_HEAP_TYPE m_DescriptorHeapType;`

`// The number of descriptors to allocate in new GPU visible descriptor heaps.`

`uint32_t` `m_NumDescriptorsPerHeap;`

`// The increment size of a descriptor.`

`uint32_t` `m_DescriptorHandleIncrementSize;`

The  `m_DescriptorHeapType`  member variable stores the type of descriptor heap the  `DynamicDescriptorHeap`  uses. This can be either  `[D3D12_DESCRIPTOR_HEAP_TYPE_CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`  or  `[D3D12_DESCRIPTOR_HEAP_TYPE_SAMPLER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`.

The  `m_NumDescriptorsPerHeap`  variable indicates how many descriptors to allocate for each descriptor heap.

The  `m_DescriptorHandleIncrementSize`  variable indicates the offset between descriptors in the descriptor heap. Since the increment size of a descriptor within a descriptor heap is vendor specific, it must be queried at runtime.

DynamicDescriptorHeap.h

1

2

3

4

5

`// The descriptor handle cache.`

`std::unique_ptr<D3D12_CPU_DESCRIPTOR_HANDLE[]> m_DescriptorHandleCache;`

`// Descriptor handle cache per descriptor table.`

`DescriptorTableCache m_DescriptorTableCache[MaxDescriptorTables];`

The  `m_DescriptorHandleCache`  variable is an array of  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`s. The number of descriptors that can be cached is determined by the  `numDescriptors`argument passed to the paramertized constructor of the  `DynamicDescriptorHeap`  class.

The  `m_DescriptorTableCache`  variable is an array of  `DescriptorTableCache`  structs. This array is statically sized to the maximum number of descriptor tables that can appear in a root signature (`MaxDescriptorTables`). The layout of the  `m_DescriptorTableCache`  array is configured in the  `ParseRootSignature`  method shown later.

DynamicDescriptorHeap.h

173

174

175

176

177

178

179

`// Each bit in the bit mask represents the index in the root signature`

`// that contains a descriptor table.`

`uint32_t` `m_DescriptorTableBitMask;`

`// Each bit set in the bit mask represents a descriptor table`

`// in the root signature that has changed since the last time the`

`// descriptors were copied.`

`uint32_t` `m_StaleDescriptorTableBitMask;`

The  `m_DescriptorTableBitMask`  variable indicates which entries in the currently bound root signature contains a descriptor table. The  `m_StaleDescriptorTableBitMask`  variable is used to indicate which descriptor table entries have been modified since the previous commit. If a root signature has multiple descriptor table entries (as is shown in the example in the  [introduction to this section](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)) but only one of the descriptor tables is modified between draw (or dispatch) commands, then only the modified descriptor table needs to be copied the GPU visible descriptor heap. Any unmodified descriptor tables can be left as-is.

DynamicDescriptorHeap.h

181

182

183

184

`using` `DescriptorHeapPool = std::queue< Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> >;`

`DescriptorHeapPool m_DescriptorHeapPool;`

`DescriptorHeapPool m_AvailableDescriptorHeaps;`

The  `DescriptorHeapPool`  is an alias type for a  `[std::queue](https://en.cppreference.com/w/cpp/container/queue)`  of  `[ID3D12DescriptorHeap](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12descriptorheap)`s.

The  `m_DescriptorHeapPool`  variable stores all of the descriptor heaps created by the  `DynamicDescriptorHeap`  class and the  `m_AvailableDescriptorHeaps`  variable stores only the descriptor heaps that still contain descriptors. When a descriptor heap does not contain enough descriptors to commit all staged descriptors to the descriptor heap then it is removed from the  `m_AvailableDescriptorHeaps`  queue until the  `DynamicDescriptorHeap`  is reset.

DynamicDescriptorHeap.h

186

187

188

189

190

191

192

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> m_CurrentDescriptorHeap;`

`CD3DX12_GPU_DESCRIPTOR_HANDLE m_CurrentGPUDescriptorHandle;`

`CD3DX12_CPU_DESCRIPTOR_HANDLE m_CurrentCPUDescriptorHandle;`

`uint32_t` `m_NumFreeHandles;`

`};`

The  `m_CurrentDescriptorHeap`  variable points to the current descriptor heap that is bound to the command list.

The  `m_CurrentGPUDescriptorHandle`  and  `m_CurrentCPUDescriptorHandle`  variables store the current GPU and CPU descriptor handles within the  `m_CurrentDescriptorHeap`descriptor heap.

The  `m_NumFreeHandles`  variable stores the number of descriptor handles that are still available in the currently bound descriptor heap.

[![Dynamic Descriptor Heap Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DynamicDescriptorHeap.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/DynamicDescriptorHeap.h)

### DYNAMICDESCRIPTORHEAP PREAMBLE

The preamble for the  `DynamicDescriptorHeap`  implementation file contains the additional headers that are required to compile the class.

DynamicDescriptorHeap.cpp

1

2

3

4

5

6

7

`#include <DX12LibPCH.h>`

`#include <DynamicDescriptorHeap.h>`

`#include <Application.h>`

`#include <CommandList.h>`

`#include <RootSignature.h>`

The  `DX12LibPCH.h`  header file is the  _precompiled header file_  for the DX12Lib project.

The  `DynamicDescriptorHeap.h`  header file contains the declaration for the  `DynamicDescriptorHeap`  class. This header file is described in the previous section.

The  `Application.h`  header file is required to get access to the  `[ID2D12Device](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12device)`  which is owned by the  `Application`  class.

The  `CommandList.h`  header file contains the declaration of the  `CommandList`  class and the  `RootSignature.h`  header file contains the declaration of the  `RootSignature`  class. These classes are part of the DX12Lib project but are not described in detail in this lesson.

### DYNAMICDESCRIPTORHEAP::DYNAMICDESCRIPTORHEAP

The constructor for the  `DynamicDescriptorHeap`  initializes the variables for the  `DynamicDescriptorHeap`  and allocates storage for the descriptor handle cache based on the maximum number of descriptors per descriptor heap.

DynamicDescriptorHeap.cpp

9

10

11

12

13

14

15

16

17

18

19

20

21

22

`DynamicDescriptorHeap::DynamicDescriptorHeap(D3D12_DESCRIPTOR_HEAP_TYPE heapType,` `uint32_t` `numDescriptorsPerHeap)`

`: m_DescriptorHeapType(heapType)`

`, m_NumDescriptorsPerHeap(numDescriptorsPerHeap)`

`, m_DescriptorTableBitMask(0)`

`, m_StaleDescriptorTableBitMask(0)`

`, m_CurrentCPUDescriptorHandle(D3D12_DEFAULT)`

`, m_CurrentGPUDescriptorHandle(D3D12_DEFAULT)`

`, m_NumFreeHandles(0)`

`{`

`m_DescriptorHandleIncrementSize = Application::Get().GetDescriptorHandleIncrementSize(heapType);`

`// Allocate space for staging CPU visible descriptors.`

`m_DescriptorHandleCache = std::make_unique<D3D12_CPU_DESCRIPTOR_HANDLE[]>(m_NumDescriptorsPerHeap);`

`}`

Since the increment size of a descriptor in a descriptor heap is vendor specific, it must be queried at runtime. The increment size of a descriptor is queried on line 18.

On line 21, the descriptor handle cache is created based on the maximum number of descriptors that can be copied to the GPU visible descriptor heap.

### DYNAMICDESCRIPTORHEAP::PARSEROOTSIGNATURE

Before any descriptors can be staged to the  `DynamicDescriptorHeap`  the layout of the descriptor tables in the root signature must be known. The  `ParseRootSignature`  method is used to configure the layout of the descriptor cache whenever the root signature is changed on the command list.

DynamicDescriptorHeap.cpp

27

28

29

30

31

32

33

`void DynamicDescriptorHeap::ParseRootSignature(``const` `RootSignature& rootSignature)`

`{`

`// If the root signature changes, all descriptors must be (re)bound to the`

`// command list.`

`m_StaleDescriptorTableBitMask = 0;`

`const` `auto& rootSignatureDesc = rootSignature.GetRootSignatureDesc();`

The only argument to the  `ParseRootSignature`  method is a reference to a  `RootSignature`. The  `RootSignature`  class is part of the DX12Lib project but is not described in any detail in this lesson. The  `RootSignature`  class provides a wrapper for a  `[ID3D12RootSignature](https://msdn.microsoft.com/en-us/library/windows/desktop/dn788714(v=vs.85).aspx)`  with some additional methods to query the layout of the root signature.

Whenever the root signature changes on the command list, any stale descriptors that were staged but not committed should be bound again to the graphics or compute pipelines. The  `m_StaleDescriptorTableBitMask`  variable is reset on line 31 to indicate that no descriptors should be copied to a GPU visible descriptor heap until new descriptors are staged to the  `DynamicDescriptorHeap`.

The  [root signature description](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_root_signature_desc1)  used to create the root signature is cached in the  `RootSignature`  class. This value is queried on line 33 so that the layout of the root signature can be determined.

DynamicDescriptorHeap.cpp

35

36

37

38

`// Get a bit mask that represents the root parameter indices that match the`

`// descriptor heap type for this dynamic descriptor heap.`

`m_DescriptorTableBitMask = rootSignature.GetDescriptorTableBitMask(m_DescriptorHeapType);`

`uint32_t` `descriptorTableBitMask = m_DescriptorTableBitMask;`

A bitmask that represents the indices of the root signature that has a descriptor table for a particular descriptor heap type is queried on line 37. The bitmask for the root signature described in  [the example above](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)  looks like this:

[![The Descriptor Table Bit Mask indicates the indices of the root signature that has a descriptor table for a particular descriptor heap type.](https://www.3dgep.com/wp-content/uploads/2018/06/Descriptor-Table-Bit-Mask.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Descriptor-Table-Bit-Mask.png)

The  `m_DescriptorTableBitMask`  variable indicates the indices of the root signature that has a descriptor table for a particular descriptor heap type.

The above image shows an example of a descriptor table bitmask for the  `[CBV_SRV_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type)`descriptor heap type shown in  [the example above](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap). In this case, the parameters at root indices 1, 2, and 3 have a descriptor table matching the heap type.

A copy of the descriptor table bitmask is initialized on line 38 so it can be scanned and cleared without modifying the class member variable.

DynamicDescriptorHeap.cpp

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

`uint32_t` `currentOffset = 0;`

`DWORD` `rootIndex;`

`while` `(_BitScanForward(&rootIndex, descriptorTableBitMask) && rootIndex < rootSignatureDesc.NumParameters)`

`{`

`uint32_t` `numDescriptors = rootSignature.GetNumDescriptors(rootIndex);`

`DescriptorTableCache& descriptorTableCache = m_DescriptorTableCache[rootIndex];`

`descriptorTableCache.NumDescriptors = numDescriptors;`

`descriptorTableCache.BaseDescriptor = m_DescriptorHandleCache.get() + currentOffset;`

`currentOffset += numDescriptors;`

`// Flip the descriptor table bit so it's not scanned again for the current index.`

`descriptorTableBitMask ^= (1 << rootIndex);`

`}`

While there are bits enabled in the  `descriptorTableBitMask`  bitmask variable, each index of the root signature is queried on line 44 for the number of descriptors in the descriptor table. The corresponding entry of the descriptor table cache is retrieved on line 46 and the number of descriptors and a pointer to the entry in the descriptor handle cache are stored on lines 47-48.

The  `[_BitScanForward](https://docs.microsoft.com/en-us/cpp/intrinsics/bitscanforward-bitscanforward64)`  function is actually a compiler intrinsic that scans a bitfield from least-significant bit (LSB) to most-significant bit (MSB) and stores the position of the first set bit in the index argument. Compiler intrinsics are usually faster than calling an equivalent function because intrinsics usually boil down to a single CPU instruction in the compiled executable.

The current offset in the descriptor handle cache is updated on line 50 by the number of descriptors in the descriptor table.

On line 53, the bit in the  `descriptorTableBitMask`  is flipped to 0 so that the current index is not scanned again in the  `while`  loop.

DynamicDescriptorHeap.cpp

56

57

58

`// Make sure the maximum number of descriptors per descriptor heap has not been exceeded.`

`assert``(currentOffset <= m_NumDescriptorsPerHeap &&` `"The root signature requires more than the maximum number of descriptors per descriptor heap. Consider increasing the maximum number of descriptors per descriptor heap."``);`

`}`

Before leaving the  `ParseRootSignature`  method, the post condition that the total number of descriptors of the root signature does not exceed the maximum number of descriptors that can be copied to the GPU visible descriptor heap is checked.

### DYNAMICDESCRIPTORHEAP::STAGEDESCRIPTORS

The  `StageDescriptors`  method is used to copy the CPU descriptor handles to prepare them for committing them to the GPU visible descriptor heap later.

DynamicDescriptorHeap.cpp

60

61

62

63

64

65

66

67

`void DynamicDescriptorHeap::StageDescriptors(``uint32_t` `rootParameterIndex,` `uint32_t` `offset,` `uint32_t` `numDescriptors,` `const` `D3D12_CPU_DESCRIPTOR_HANDLE srcDescriptor)`

`{`

`// Cannot stage more than the maximum number of descriptors per heap.`

`// Cannot stage more than MaxDescriptorTables root parameters.`

`if` `(numDescriptors > m_NumDescriptorsPerHeap || rootParameterIndex >= MaxDescriptorTables )`

`{`

`throw` `std::bad_alloc();`

`}`

Before copying any descriptors, the preconditions of the arguments are checked to ensure the user is not able to copy more descriptors than can fit in a descriptor heap or tries to set descriptors at an invalid index in the descriptor table cache. If either of these is the case, a  `[std::bad_alloc](https://en.cppreference.com/w/cpp/memory/new/bad_alloc)`  exception is thrown.

DynamicDescriptorHeap.cpp

69

70

71

72

73

74

75

76

`DescriptorTableCache& descriptorTableCache = m_DescriptorTableCache[rootParameterIndex];`

`// Check that the number of descriptors to copy does not exceed the number`

`// of descriptors expected in the descriptor table.`

`if` `( (offset + numDescriptors) > descriptorTableCache.NumDescriptors)`

`{`

`throw` `std::length_error(``"Number of descriptors exceeds the number of descriptors in the descriptor table."``);`

`}`

A reference to the corresponding entry in the descriptor table cache is retrieved on line 69 and an additional check to ensure the user isn't copying more descriptors than the current descriptor table is configured for is made on lines 73-76. If the user tries to copy a descriptor beyond the number of descriptors in the descriptor table, an  `[std::length_error](https://en.cppreference.com/w/cpp/error/length_error)`  exception is thrown.

DynamicDescriptorHeap.cpp

78

79

80

81

82

`D3D12_CPU_DESCRIPTOR_HANDLE* dstDescriptor = (descriptorTableCache.BaseDescriptor + offset);`

`for` `(``uint32_t` `i = 0; i < numDescriptors; ++i)`

`{`

`dstDescriptor[i] = CD3DX12_CPU_DESCRIPTOR_HANDLE(srcDescriptor, i, m_DescriptorHandleIncrementSize);`

`}`

A pointer to the descriptor handle at a particular offset in the descriptor table cache is retrieved on line 78.

On lines 79-82 the descriptor handles are copied to the descriptor handle cache.

DynamicDescriptorHeap.cpp

84

85

86

87

`// Set the root parameter index bit to make sure the descriptor table`

`// at that index is bound to the command list.`

`m_StaleDescriptorTableBitMask |= (1 << rootParameterIndex);`

`}`

To ensure the staged descriptors are committed to the GPU visible descriptor heap when the  `CommitStagedDescriptors`  method is invoked, the corresponding bit in the  `m_StaleDescriptorTableBitMask`  variable is set to 1 on line 86.

### DYNAMICDESCRIPTORHEAP::COMPUTESTALEDESCRIPTORCOUNT

The  `ComputeStaleDescriptorCount`  method is used to determine the number of descriptors that need to be committed to the GPU visible descriptor heap.

DynamicDescriptorHeap.cpp

89

90

91

92

93

94

95

96

97

98

99

100

101

102

`uint32_t` `DynamicDescriptorHeap::ComputeStaleDescriptorCount()` `const`

`{`

`uint32_t` `numStaleDescriptors = 0;`

`DWORD` `i;`

`DWORD` `staleDescriptorsBitMask = m_StaleDescriptorTableBitMask;`

`while` `( _BitScanForward( &i, staleDescriptorsBitMask ) )`

`{`

`numStaleDescriptors += m_DescriptorTableCache[i].NumDescriptors;`

`staleDescriptorsBitMask ^= ( 1 << i );`

`}`

`return` `numStaleDescriptors;`

`}`

The  `ComputeStaleDescriptorCount`  method is fairly simple. It counts the number of descriptors in any descriptor table cache whose corresponding bit in the  `m_StaleDescriptorTableBitMask`  is set.

### DYNAMICDESCRIPTORHEAP::REQUESTDESCRIPTORHEAP

The  `RequestDescriptorHeap`  method retrieves a descriptor heap from the list of availble descriptor heaps. If there are no descriptor heaps available, a new one is created.

DynamicDescriptorHeap.cpp

104

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> DynamicDescriptorHeap::RequestDescriptorHeap()`

`{`

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> descriptorHeap;`

`if` `(!m_AvailableDescriptorHeaps.empty())`

`{`

`descriptorHeap = m_AvailableDescriptorHeaps.front();`

`m_AvailableDescriptorHeaps.pop();`

`}`

`else`

`{`

`descriptorHeap = CreateDescriptorHeap();`

`m_DescriptorHeapPool.push(descriptorHeap);`

`}`

`return` `descriptorHeap;`

`}`

If the  `m_AvailableDescriptorHeaps`  queue is not empty, then the first element is popped off the queue. If the  `m_AvailableDescriptorHeaps`  queue is empty, then a new descriptor heap is created on 114 and added to the  `m_DescriptorHeapPool`.

### DYNAMICDESCRIPTORHEAP::CREATEDESCRIPTORHEAP

If the  `m_AvailableDescriptorHeaps`  queue is empty, then a new descriptor heap is crated using the  `CreateDescriptorHeap`  method.

DynamicDescriptorHeap.cpp

121

122

123

124

125

126

127

128

129

130

131

132

133

134

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> DynamicDescriptorHeap::CreateDescriptorHeap()`

`{`

`auto device = Application::Get().GetDevice();`

`D3D12_DESCRIPTOR_HEAP_DESC descriptorHeapDesc = {};`

`descriptorHeapDesc.Type = m_DescriptorHeapType;`

`descriptorHeapDesc.NumDescriptors = m_NumDescriptorsPerHeap;`

`descriptorHeapDesc.Flags = D3D12_DESCRIPTOR_HEAP_FLAG_SHADER_VISIBLE;`

`Microsoft::WRL::ComPtr<ID3D12DescriptorHeap> descriptorHeap;`

`ThrowIfFailed(device->CreateDescriptorHeap(&descriptorHeapDesc, IID_PPV_ARGS(&descriptorHeap)));`

`return` `descriptorHeap;`

`}`

Descriptor heap creation is described in detail in the  [first lesson in this series](https://www.3dgep.com/learning-directx12-1/#Create_a_Descriptor_Heap). What is interesting to note here is that the descriptor heap is created with the  `[D3D12_DESCRIPTOR_HEAP_FLAG_SHADER_VISIBLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_flags)`  flag which enables these descriptors to be mapped to the command list and used to access resources in a HLSL shader.

### DYNAMICDESCRIPTORHEAP::COMMITSTAGEDDESCRIPTORS

Arguably the most interesting (and most complex) method of the  `DynamicDescriptorHeap`  class is the  `CommitStagedDescriptors`  method. This method copies the staged descriptors in the descriptor table cache to the GPU visible descriptor heap and binds the descriptors to the command list using the appropriate method.

DynamicDescriptorHeap.cpp

136

137

138

139

`void DynamicDescriptorHeap::CommitStagedDescriptors(CommandList& commandList, std::function<void(ID3D12GraphicsCommandList*,` `UINT``, D3D12_GPU_DESCRIPTOR_HANDLE)> setFunc)`

`{`

`// Compute the number of descriptors that need to be copied`

`uint32_t` `numDescriptorsToCommit = ComputeStaleDescriptorCount();`

The  `CommitStagedDescriptors`  method takes two parameters: the command list used to bind the descriptors and a setter function that is either  `[ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setgraphicsrootdescriptortable)`  or  `[ID3D12GraphicsCommandList::SetComputeRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setcomputerootdescriptortable)`  depending on the command being executed on the command list.

The  `DynamicDescriptorHeap::CommitStagedDescriptors`  method should not be called directly. The  `DynamicDescriptorHeap::CommitStagedDescriptorsForDraw`and the  `DynamicDescriptorHeap::CommitStagedDescriptorsForDispatch`  should be used instead.  

The number of descriptors that need to be committed is computed on line 139 using the  `[ComputeStaleDescriptorCount](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapComputeStaleDescriptorCount)`  method described earlier.

DynamicDescriptorHeap.cpp

141

142

143

144

145

`if` `( numDescriptorsToCommit > 0 )`

`{`

`auto device = Application::Get().GetDevice();`

`auto d3d12GraphicsCommandList = commandList.GetGraphicsCommandList().Get();`

`assert``(d3d12GraphicsCommandList != nullptr);`

If there are no descriptors to commit, the  `CommitStagedDescriptors`  method should do nothing. The  `[ID3D12Device](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12device)`  is retrieved from the  `Application`  class on line 143 and a pointer to the  `[ID3D12GraphicsCommandList](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12graphicscommandlist)`  is retrieved on 144. On line 145, the pointer to the  `[ID3D12GraphicsCommandList](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12graphicscommandlist)`  is checked to make sure it is not null.

DynamicDescriptorHeap.cpp

147

148

149

150

151

152

153

154

155

156

157

158

159

160

`if` `( !m_CurrentDescriptorHeap || m_NumFreeHandles < numDescriptorsToCommit )`

`{`

`m_CurrentDescriptorHeap = RequestDescriptorHeap();`

`m_CurrentCPUDescriptorHandle = m_CurrentDescriptorHeap->GetCPUDescriptorHandleForHeapStart();`

`m_CurrentGPUDescriptorHandle = m_CurrentDescriptorHeap->GetGPUDescriptorHandleForHeapStart();`

`m_NumFreeHandles = m_NumDescriptorsPerHeap;`

`commandList.SetDescriptorHeap(m_DescriptorHeapType, m_CurrentDescriptorHeap.Get());`

`// When updating the descriptor heap on the command list, all descriptor`

`// tables must be (re)recopied to the new descriptor heap (not just`

`// the stale descriptor tables).`

`m_StaleDescriptorTableBitMask = m_DescriptorTableBitMask;`

`}`

If either the  `m_CurrentDescriptorHeap`  is null (which is the case when the  `DynamicDescriptorHeap`  is first created or after it has been reset) or there are not enough free handles to commit to the descriptor heap, a new heap retrieved using the  `RequestDescriptorHeap`  method on line 149.

On lines 150-151 the CPU and GPU descriptor handles are set to the first descriptors in the new heap and the number of free handles is reset to the total number of descriptors in the descriptor heap.

The  `CommandList::SetDescriptorHeap`  method is used to ensure the command list has the new descriptor heap bound.

When changing descriptor heaps, it is necessary to copy  _all_  of the staged descriptors to the descriptor heap (not just the ones that have been updated since the last time the descriptors were committed). Resetting the  `m_StaleDescriptorTableBitMask`  variable to the value of the  `m_DescriptorTableBitMask`  on line 159 ensures that all of the staged descriptors are copied to the new descriptor heap.

DynamicDescriptorHeap.cpp

162

163

164

165

166

167

`DWORD` `rootIndex;`

`// Scan from LSB to MSB for a bit set in staleDescriptorsBitMask`

`while` `( _BitScanForward( &rootIndex, m_StaleDescriptorTableBitMask ) )`

`{`

`UINT` `numSrcDescriptors = m_DescriptorTableCache[rootIndex].NumDescriptors;`

`D3D12_CPU_DESCRIPTOR_HANDLE* pSrcDescriptorHandles = m_DescriptorTableCache[rootIndex].BaseDescriptor;`

The  `[_BitScanForward](https://docs.microsoft.com/en-us/cpp/intrinsics/bitscanforward-bitscanforward64)`  intrinsic method is used to iterate the stale descriptor tables that need to be committed to the GPU visible desccriptor heap.

On lines 166-165, the number of descriptors and the pointer to the CPU visible descriptors in the descriptor table cache is retrieved.

DynamicDescriptorHeap.cpp

169

170

171

172

173

174

175

176

`D3D12_CPU_DESCRIPTOR_HANDLE pDestDescriptorRangeStarts[] =`

`{`

`m_CurrentCPUDescriptorHandle`

`};`

`UINT` `pDestDescriptorRangeSizes[] =`

`{`

`numSrcDescriptors`

`};`

Before the descriptors are copied to the GPU visible descriptor heap, it is necssary to configure an array that contains the destination descriptor handles and an array that contains the destination descriptor ranges.

DynamicDescriptorHeap.cpp

178

179

180

`// Copy the staged CPU visible descriptors to the GPU visible descriptor heap.`

`device->CopyDescriptors(1, pDestDescriptorRangeStarts, pDestDescriptorRangeSizes,`

`numSrcDescriptors, pSrcDescriptorHandles, nullptr, m_DescriptorHeapType);`

The CPU descriptor handles are copied to the GPU visible descriptor heap on line 178 using the  `[ID3D12Device::CopyDescriptors](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-copydescriptors)`  method. This method has the following signature  [[4]](https://www.3dgep.com/learning-directx12-3/#cite-4):

ID3D12Device::CopyDescriptors method

1

2

3

4

5

6

7

8

9

`void CopyDescriptors(`

`UINT` `NumDestDescriptorRanges,`

`const` `D3D12_CPU_DESCRIPTOR_HANDLE *pDestDescriptorRangeStarts,`

`const` `UINT` `*pDestDescriptorRangeSizes,`

`UINT` `NumSrcDescriptorRanges,`

`const` `D3D12_CPU_DESCRIPTOR_HANDLE *pSrcDescriptorRangeStarts,`

`const` `UINT` `*pSrcDescriptorRangeSizes,`

`D3D12_DESCRIPTOR_HEAP_TYPE DescriptorHeapsType`

`);`

And takes the following arguments:

-   `UINT NumDestDescriptorRanges`: The number of destination descriptor ranges to copy to. In this case, there is only 1 destintion descriptor range.
-   `const [D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle) *pDestDescriptorRangeStarts`: An array of  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`s to copy to.
-   `const UINT *pDestDescriptorRangeSizes`: An array of destination descriptor range sizes to copy to.
-   `UINT NumSrcDescriptorRanges`: The number of source descriptor ranges to copy from. There is no requirement that the source descriptors appear contigiously in the same CPU visible descriptor heap (or that they come from the same descriptor heap) the number of source ranges is equal to the number of descriptors to copy. That is, the size of each source descriptor range is 1.
-   `const [D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle) *pSrcDescriptorRangeStarts`: An array of  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`s to copy from.
-   `const UINT *pSrcDescriptorRangeSizes`: An array of source descriptor range sizes to copy from. This parameter is optional and if null, then each descriptor range size is considered to be 1 and the descriptors are copied one at a time. Since the source descriptors do not appear in a consecutive range in the source descriptor heaps, this behaviour is exactly what is required.
-   `[D3D12_DESCRIPTOR_HEAP_TYPE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type) DescriptorHeapsType`: Specifies the type of descriptor heap to copy with.

DynamicDescriptorHeap.cpp

182

183

`// Set the descriptors on the command list using the passed-in setter function.`

`setFunc(d3d12GraphicsCommandList, rootIndex, m_CurrentGPUDescriptorHandle);`

Using the setter function passed to the  `CommitStagedDescriptors`  method, the GPU visible descriptors are set on the command list.

DynamicDescriptorHeap.cpp

185

186

187

188

`// Offset current CPU and GPU descriptor handles.`

`m_CurrentCPUDescriptorHandle.Offset(numSrcDescriptors, m_DescriptorHandleIncrementSize);`

`m_CurrentGPUDescriptorHandle.Offset(numSrcDescriptors, m_DescriptorHandleIncrementSize);`

`m_NumFreeHandles -= numSrcDescriptors;`

The current CPU and GPU descriptor handles are incremented on lines 186-187 by the number of descriptors that were copied and the number of free handles in the current descriptor heap is decremented on line 188.

DynamicDescriptorHeap.cpp

1

2

3

4

5

`// Flip the stale bit so the descriptor table is not recopied again unless it is updated with a new descriptor.`

`m_StaleDescriptorTableBitMask ^= (1 << rootIndex);`

`}`

`}`

`}`

To ensure the current descriptor table is not copied again (unless the descriptors are updated) the corresponding bit in the  `m_StaleDescriptorTableBitMask`  bitmask is inverted on line 191.

### DYNAMICDESCRIPTORHEAP::COMMITSTAGEDDESCRIPTORSFORDRAW

The  `CommitStagedDescriptorsForDraw`  method is a helper method that forwards the  `[ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setgraphicsrootdescriptortable)`  method to the  `[CommitStagedDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptors)`  method.

DynamicDescriptorHeap.cpp

196

197

198

199

`void DynamicDescriptorHeap::CommitStagedDescriptorsForDraw(CommandList& commandList)`

`{`

`CommitStagedDescriptors(commandList, &ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable);`

`}`

### DYNAMICDESCRIPTORHEAP::COMMITSTAGEDDESCRIPTORSFORDISPATCH

The  `CommitStagedDescriptorsForDispatch`  method is a helper method that forwards the  `[ID3D12GraphicsCommandList::SetComputeRootDescriptorTable](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setcomputerootdescriptortable)`  method to the  `[CommitStagedDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptors)`  method.

DynamicDescriptorHeap.cpp

201

202

203

204

`void DynamicDescriptorHeap::CommitStagedDescriptorsForDispatch(CommandList& commandList)`

`{`

`CommitStagedDescriptors(commandList, &ID3D12GraphicsCommandList::SetComputeRootDescriptorTable);`

`}`

### DYNAMICDESCRIPTORHEAP::COPYDESCRIPTOR

The  `CopyDescriptor`  method is used to copy a single CPU visible descriptor to a GPU visible descriptor heap.

DynamicDescriptorHeap.cpp

206

207

208

209

210

211

212

213

214

215

216

217

218

219

220

221

`D3D12_GPU_DESCRIPTOR_HANDLE DynamicDescriptorHeap::CopyDescriptor(CommandList& comandList, D3D12_CPU_DESCRIPTOR_HANDLE cpuDescriptor)`

`{`

`if` `(!m_CurrentDescriptorHeap || m_NumFreeHandles < 1)`

`{`

`m_CurrentDescriptorHeap = RequestDescriptorHeap();`

`m_CurrentCPUDescriptorHandle = m_CurrentDescriptorHeap->GetCPUDescriptorHandleForHeapStart();`

`m_CurrentGPUDescriptorHandle = m_CurrentDescriptorHeap->GetGPUDescriptorHandleForHeapStart();`

`m_NumFreeHandles = m_NumDescriptorsPerHeap;`

`comandList.SetDescriptorHeap(m_DescriptorHeapType, m_CurrentDescriptorHeap.Get());`

`// When updating the descriptor heap on the command list, all descriptor`

`// tables must be (re)recopied to the new descriptor heap (not just`

`// the stale descriptor tables).`

`m_StaleDescriptorTableBitMask = m_DescriptorTableBitMask;`

`}`

Similar to the  `CommitStagedDescriptors`  method, there must be at least one descriptor avaiable in the currently bound descriptor heap. If the current descriptor heap is not valid or there are no free descriptors in the descirptor heap, a new descriptor heap is requested on line 210. If the current descriptor heap changes, then the new descriptor heap must be updated on the command list. It is also important to reset the  `m_StaleDescriptorTableBitMask`  to ensure that all descriptors are copied to the new GPU visible descriptor heap before a draw or dispatch command is executed on the command list.

DynamicDescriptorHeap.cpp

223

224

225

226

227

228

229

230

231

232

233

`auto device = Application::Get().GetDevice();`

`D3D12_GPU_DESCRIPTOR_HANDLE hGPU = m_CurrentGPUDescriptorHandle;`

`device->CopyDescriptorsSimple(1, m_CurrentCPUDescriptorHandle, cpuDescriptor, m_DescriptorHeapType);`

`m_CurrentCPUDescriptorHandle.Offset(1, m_DescriptorHandleIncrementSize);`

`m_CurrentGPUDescriptorHandle.Offset(1, m_DescriptorHandleIncrementSize);`

`m_NumFreeHandles -= 1;`

`return` `hGPU;`

`}`

Since only a single descriptor is being copied from the source descriptor to the destination descriptor the  `[ID3D12Device::CopyDescriptorsSimple](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-copydescriptorssimple)`  method is used. This method has the following signature  [[5]](https://www.3dgep.com/learning-directx12-3/#cite-5):

ID3D12Device::CopyDescriptorsSimple method

1

2

3

4

5

6

`void CopyDescriptorsSimple(`

`UINT` `NumDescriptors,`

`D3D12_CPU_DESCRIPTOR_HANDLE DestDescriptorRangeStart,`

`D3D12_CPU_DESCRIPTOR_HANDLE SrcDescriptorRangeStart,`

`D3D12_DESCRIPTOR_HEAP_TYPE DescriptorHeapsType`

`);`

And takes the following parameters:

-   `UINT NumDescriptors`: The number of descriptors to copy. Both source and destination descriptors are considered to be consecutively ordered in the descriptor heap.
-   `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle) DestDescriptorRangeStart`: A  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  that describes the destination descriptors to start to copy to.
-   `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle) SrcDescriptorRangeStart`: A  `[D3D12_CPU_DESCRIPTOR_HANDLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_cpu_descriptor_handle)`  that describes the source descriptors to start to copy from.
-   `[D3D12_DESCRIPTOR_HEAP_TYPE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_heap_type) DescriptorHeapsType`: Specifies the type of descriptor heap to copy with.

After copying the descriptor to the GPU visible descriptor heap, the current CPU and GPU handles are incremented, the number free handles is decremented, and the GPU descriptor handle is returned on line 232.

### DYNAMICDESCRIPTORHEAP::RESET

The  `Reset`  method is called on the  `DynamicDescriptorHeap`  class when the commands that are referencing any descriptor in the  `DynamicDescriptorHeap`  have finished executing on the GPU. When the  `DynamicDescriptorHeap`  is reset, all of the descriptor heaps are made avaiable again and the descriptor table cache is reset.

DynamicDescriptorHeap.cpp

235

236

237

238

239

240

241

242

243

244

245

246

247

248

249

250

`void DynamicDescriptorHeap::Reset()`

`{`

`m_AvailableDescriptorHeaps = m_DescriptorHeapPool;`

`m_CurrentDescriptorHeap.Reset();`

`m_CurrentCPUDescriptorHandle = CD3DX12_CPU_DESCRIPTOR_HANDLE(D3D12_DEFAULT);`

`m_CurrentGPUDescriptorHandle = CD3DX12_GPU_DESCRIPTOR_HANDLE(D3D12_DEFAULT);`

`m_NumFreeHandles = 0;`

`m_DescriptorTableBitMask = 0;`

`m_StaleDescriptorTableBitMask = 0;`

`// Reset the table cache`

`for` `(``int` `i = 0; i < MaxDescriptorTables; ++i)`

`{`

`m_DescriptorTableCache[i].Reset();`

`}`

`}`

On line 237 the  `m_DescriptorHeapPool`  (which is a  `[queue](https://en.cppreference.com/w/cpp/container/queue)`  that contains all of the descriptor heaps created by the  `DynamicDescriptorHeap`  class) is copied to the  `m_AvailableDescriptorHeaps`  `[queue](https://en.cppreference.com/w/cpp/container/queue)`  effectively making all of the descriptor heaps avaialable again and ready for new allocations.

On line 238 the (`[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class)`) for the current descriptor heap is reset. This ensures that a request for an available descriptor heap is made when descriptors are copied (using either the  `[CommitStagedDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptors)`  method or the  `[CopyDescriptor](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCopyDescriptor)`  method).

On lines 239-243, the descriptor handles, number of free descriptors, and descriptor table bit masks are all reset.

On lines 246-249, the descriptor table cache is reset (removing all descriptor table entries from the descriptor table cache). Before any new descriptors can be stagged to the  `DynamicDescriptorHeap`, a root signature must be parsed using the  `[ParseRootSignature](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapParseRootSignature)`  method.

This concludes the description of the  `DynamicDescriptorHeap`  class. In the next section, the  `ResourceStateTracker`  is described. The  `ResourceStateTracker`  class is used to track state transitions for (sub)resources.

[![Dynamic Descriptor Heap Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for DynamicDescriptorHeap.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/DynamicDescriptorHeap.cpp)

# Resource State Tracking

Resource barriers are briefly discussed in  [Lesson 1](https://www.3dgep.com/learning-directx12-1/#Render). If you are unsure what a resource barrier is, please read that section first.  

In previous version of DirectX, the state of a resource was automatically tracked by the graphics driver. Since DirectX 12, it is the responsibility of the graphics programmer to transition resources to the correct state before using the resource on the command list.

Certain operations can only be performed on a resource if the resource is in the correct state. For example, before a resource can be used for reading in a pixel shader, the resource must be in the  `[D3D12_RESOURCE_STATE_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state and before a resource can be written to in a compute shader, the resource must be in the  `[D3D12_RESOURCE_STATE_UNORDERED_ACCESS](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state. In a single-threaded environment, keeping track of the state of a resource is trivial since all operations on a resource generally occur in linear order. In a multi-threaded environment however it is possible that a resource must be in the  `[D3D12_RESOURCE_STATE_DEPTH_WRITE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state in one thread but needs to be in the  `[D3D12_RESOURCE_STATE_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  in another thread at the same time (this is common for performing shadow mapping for example).

When transitioning a resource to another state, both the  _before_  and  _after_  states must be known. It becomes even more complicated since each subresource of a resource can be in a different state. For example, when performing mipmapping in a compute shader, the first subresource of a texture should be in the  `[D3D12_RESOURCE_STATE_NON_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  so that it can be read from in a compute shader and the other subresoruces should be in the  `[D3D12_RESOURCE_STATE_UNORDERED_ACCESS](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state so that they can be written to in a compute shader.

Tracking the state of a resource (and all of its subresources) across multiple command lists and multiple threads can be tedious and error prone. The purpose of the  `ResourceStateTracker`  class is to track the state of a resource within a command list and to ensure correct resource state transitions even when the resource is being used in different states on different threads.

The  `ResourceStateTracker`  class tracks the state of a resource within a command list. The class shown here is intended to be used by the custom  `CommandList`  class that is described later in this lesson. It is not intended to be used outside of the  `CommandList`  class and certain assumptions have been made in the design of the  `ResourceStateTracker`  class. For example, while it is possible to build different command lists across different threads, a single command list will not be shared across multiple threads (command list building is a single-threaded operation). This allows for some simplifying assumptions such as the state of a resource will not be modified by multiple threads  _within the same command list_.  

The design of the  `ResourceStateTracker`  class described here is influenced by "the inimitable" Sebastian Merry in  [his YouTube video about resource barriers and resource state tracking](https://youtu.be/nmB2XMasz2o)  which can be seen here:  [https://youtu.be/nmB2XMasz2o](https://youtu.be/nmB2XMasz2o).

When submitting a resource state transition barrier to the  `ResourceStateTracker`, it first checks if the resource has been used on the current command list before. If the resource has not been used on the command list yet, it adds the transition barrier to a list of  _pending_  barriers (which are not directly added to the command list) and it adds the  _after_  state of the resource to a list of "known state" for that resource. The next time a transition barrier is sent to the  `ResourceStateTracker`  for the same resource, it uses the known state of the resource as the  _before_  state for the transition and adds the barrier to the command list.

When submitting the command list to the command queue for execution, the  _pending_barriers are compared against the  _global state_  of the resource. If the  _global state_  and the  _pending state_  are different, then the pending barrier is added to another command list that is inserted into the command queue before the command list that is being executed.

[![Command List (A) is built on CPU thread 0 and Command List (B) is built on CPU thread 1. Both Command List (A) and Command List (B) are executed sequentially on the GPU.](https://www.3dgep.com/wp-content/uploads/2018/06/Resource-State-Tracker.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Resource-State-Tracker.png)

Command List (A) is built on CPU thread 0 and Command List (B) is built on CPU thread 1. Both Command List (A) and Command List (B) are executed sequentially on the GPU.

The image above depicts two command lists (A and B) being built on seperate threads. Both command lists are accessing the same resource but each command lists requires the resource to be in a different state. In this case, Command List B does not know what state Command List A left the resource in. To ensure the resource is transitioned to the correct state required by Command List B, an intermediate Command List (C) is injected into the command queue between A and B.

[![An intermediate Command List (C) is injected into the Command Queue ensuring resources used by Command List B are in the correct state.](https://www.3dgep.com/wp-content/uploads/2018/06/Resource-State-Tracker-2.png)](https://www.3dgep.com/wp-content/uploads/2018/06/Resource-State-Tracker-2.png)

An intermediate Command List (C) is injected into the Command Queue ensuring resources used by Command List B are in the correct state.

The singular purpose of the intermediate Command List (C) is to ensure that any resources used by Command List B are in the correct state before executing the command list on the command queue.

To implement this strategy, several data structures are required:

1.  **Pending Resource Transition Barriers Array**: If, during command list building, a resource is being bound on a command list for the first time, its previous state is unknown and a transition barrier to transition the resource into the expected state is added to the  **Pending Resource Transition Barriers Array**. Pending resource transition barriers should not be confused with  [split barriers](https://docs.microsoft.com/en-us/windows/desktop/direct3d12/using-resource-barriers-to-synchronize-resource-states-in-direct3d-12#split-barriers). Split barriers are not used by the  `ResourceStateTracker` class.
2.  **Final Resource State Map**: After a resource has been used on the command list at least once, its  _final known_  state is added to the  **Final Resource State Map**indexed by a pointer to the resource.
3.  **Resource Transition Barriers Array**: If the state of a resource is known (it has an entry in the  **Final Resource State Map**) then any resource state transition is added to the  **Resource Transition Barriers Array**  and added directly to the command list before a draw or dispatch command is executed (or any command that requires transition barriers to be committed to the command list).
4.  **Global Resource State Map**: A command list may contain any number of state transitions for a resource. When a command list is executed on the command queue, the last known state of the resource is committed to the  **Global Resource State Map**. It is the  **Global Resource State Map**  that is used to determine if a Pending Resource Transition Barrier is added to the intermediate command list or not.

## ResourceStateTracker Class

The interface of the  `ResourceStateTracker`  class is fairly simple. It provides a method to add a resource barrier to the state tracker and several helper methods that allow specific barrier types (transition, UAV, or alias) to be added to the resource state tracker. The  `ResourceStateTracker`  class also provides a method to flush any pending resource barriers. Flushing of pending resource barriers is only needs to be done when the command list is executed on the command queue. Flushing of pending resource barriers is handled automatically by the  `CommandList`  class which is described later in this lesson.

The  `ResourceStateTracker`  class also provides a method to flush  _non-pending_  resource barriers to the command list. A  _non-pending_  resource barrier is any UAV, aliasing, or transition barrier where the  _before_  state of the resource is already known.

The  `ResourceStateTracker`  class also exposes a few methods to commit the final resource states to the global resource state map and to register and unregister resources to the  _global resource state map_  (when a resource is created, it is added to the global resource state map and when it is destroyed, it is removed from the global resource state map).

### RESOURCESTATETRACKER HEADER

The  `ResourceStateTracker`  has a few dependencies on external libraries. Those dependencies are included first.

ResourceStateTracker.h

47

48

49

50

51

52

53

54

55

`#include <d3d12.h>`

`#include <mutex>`

`#include <map>`

`#include <unordered_map>`

`#include <vector>`

`class` `CommandList;`

`class` `Resource;`

The  `d3d12.h`  header file is included on line 47 for the  `[D3D12_RESOURCE_STATES](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`,  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`, and  `[ID3D12Resource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12resource)`  types.

The  `[mutex](https://en.cppreference.com/w/cpp/header/mutex)`  header file is required for the  `[std::mutex](https://en.cppreference.com/w/cpp/thread/mutex)`  type which is used to syncronize access to the  _global resource state map_.

The  `[map](https://en.cppreference.com/w/cpp/header/map)`  and  `[unordered_map](https://en.cppreference.com/w/cpp/header/unordered_map)`  header files are required for the  `[std::map](https://en.cppreference.com/w/cpp/container/map)`  and  `[std::unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map)`  types used for the  _global resource state map_.

The  `[vector](https://en.cppreference.com/w/cpp/header/vector)`  header file is required for the  `[std::vector](https://en.cppreference.com/w/cpp/container/vector)`  type that is used for the  _pending_  and  _non-pending resource barriers_.

Since the  `CommandList`  and  `Resource`  types are only used as pointer or reference types in the header, it is sufficient to forward-declare these types in the header file for the  `ResourceStateTracker`  class.

ResourceStateTracker.h

57

58

59

60

61

`class` `ResourceStateTracker`

`{`

`public``:`

`ResourceStateTracker();`

`virtual` `~ResourceStateTracker();`

The declaration for the  `ResourceStateTracker`  class starts with the constructor and destructor declared on lines 60-61.

ResourceStateTracker.h

63

64

65

66

67

68

`/**`

`* Push a resource barrier to the resource state tracker.`

`*`

`* @param barrier The resource barrier to push to the resource state tracker.`

`*/`

`void ResourceBarrier(``const` `D3D12_RESOURCE_BARRIER& barrier);`

The  `ResourceBarrier`  method is used to push any type of resource barrier (transition, UAV, or alias) to the  `ResourceStateTracker`. The  `ResourceStateTracker`  also has a few methods to push specific barrier types.

ResourceStateTracker.h

70

71

72

73

74

75

76

77

78

79

`/**`

`* Push a transition resource barrier to the resource state tracker.`

`*`

`* @param resource The resource to transition.`

`* @param stateAfter The state to transition the resource to.`

`* @param subResource The subresource to transition. By default, this is D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES`

`* which indicates that all subresources should be transitioned to the same state.`

`*/`

`void TransitionResource( ID3D12Resource* resource, D3D12_RESOURCE_STATES stateAfter,` `UINT` `subResource = D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES );`

`void TransitionResource(``const` `Resource& resource, D3D12_RESOURCE_STATES stateAfter,` `UINT` `subResource = D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES);`

The  `TransitionResource`  methods are used to forward a  _transition_  resource barrrier to the  `ResourceBarrier`  method. By default, all subresources of a resource are transitioned to the same state. Notice that the  `TransitionResource`  method does not need to know the  _before_  state of the transition barrier. This is because the  `ResourceStateTracker`  is able to resolve the  _before_  state of the (sub)resource before the resource barrier is added to the command list.

ResourceStateTracker.h

81

82

83

84

85

86

87

`/**`

`* Push a UAV resource barrier for the given resource.`

`*`

`* @param resource The resource to add a UAV barrier for. Can be NULL which`

`* indicates that any UAV access could require the barrier.`

`*/`

`void UAVBarrier(``const` `Resource* resource = nullptr);`

The  `UAVBarrier`  method is used to add a UAV barrier to the resource state tracker. UAV barriers are briefly discussed in  [Lesson 1](https://www.3dgep.com/learning-directx12-1/#Render).

ResourceStateTracker.h

89

90

91

92

93

94

95

96

97

98

`/**`

`* Push an aliasing barrier for the given resource.`

`*`

`* @param beforeResource The resource currently occupying the space in the heap.`

`* @param afterResource The resource that will be occupying the space in the heap.`

`*`

`* Either the beforeResource or the afterResource parameters can be NULL which`

`* indicates that any placed or reserved resource could cause aliasing.`

`*/`

`void AliasBarrier(``const` `Resource* resourceBefore = nullptr,` `const` `Resource* resourceAfter = nullptr);`

The  `AliasBarrier`  method is used to add an aliasing barrier to the resource state tracker. Neither UAV nor aliasing barriers need to track the state of a resource so it is not strictly necessary to use the  `ResourceStateTracker`  class for those barrier types. The  `UAVBarrier`  and  `AliasBarrier`  methods are provided by the  `ResourceStateTracker`  class so that resource barriers are managed in a consistent way and to ensure that resource barriers are aggregated to minimize the number of calls to the  `[ID3D12GraphicsCommandList::ResourceBarrier](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-resourcebarrier)`  method (which is recommended).

ResourceStateTracker.h

100

101

102

103

104

105

`/**`

`* Flush any pending resource barriers to the command list.`

`*`

`* @return The number of resource barriers that were flushed to the command list.`

`*/`

`uint32_t` `FlushPendingResourceBarriers(CommandList& commandList);`

The  `FlushPendingResourceBarriers`  method is used to flush any pending resource barriers to the specified command list. This method is called just after the command list is closed and just before it is executed on the command queue.

ResourceStateTracker.h

107

108

109

110

111

`/**`

`* Flush any (non-pending) resource barriers that have been pushed to the resource state`

`* tracker.`

`*/`

`void FlushResourceBarriers(CommandList& commandList);`

The  `FlushResourceBarriers`  method is used to flush any non-pending resource barriers to the specified command list.

ResourceStateTracker.h

113

114

115

116

117

`/**`

`* Commit final resource states to the global resource state map.`

`* This must be called when the command list is closed.`

`*/`

`void CommitFinalResourceStates();`

The  `CommitFinalResourceStates`  method is used to update the global resource state map with the final known states of the resources.

ResourceStateTracker.h

119

120

121

122

`/**`

`* Reset state tracking. This must be done when the command list is reset.`

`*/`

`void Reset();`

The  `Reset`  method is called on the  `ResourceStateTracker`  whenever the command list that owns the  `ResourceStateTracker`  is reset. This ensures the pending, non-pending, and final resource state arrays are all reset.

ResourceStateTracker.h

124

125

126

127

128

129

130

131

132

133

134

135

136

`/**`

`* The global state must be locked before flushing pending resource barriers`

`* and committing the final resource state to the global resource state.`

`* This ensures consistency of the global resource state between command list`

`* executions.`

`*/`

`static` `void Lock();`

`/**`

`* Unlocks the global resource state after the final states have been committed`

`* to the global resource state array.`

`*/`

`static` `void Unlock();`

In order to ensure consistent resource state across multiple threads, the global resource state map must be locked before pending resource barriers are flushed (since this requires reading from the global resource state map) and before flushing the final resource states to the global resource state map. The  `Lock`  method ensures that the current thread has exclusive ownership of the global resource state map and the  `Unlock`  method releases control allowing other threads to access the global resource state map. A  `[std::mutex](https://en.cppreference.com/w/cpp/thread/mutex)`  is used to ensure exclusive ownership of the global resource state map.

ResourceStateTracker.h

1

2

3

4

5

6

7

8

9

10

11

`/**`

`* Add a resource with a given state to the global resource state array (map).`

`* This should be done when the resource is created for the first time.`

`*/`

`static` `void AddGlobalResourceState(ID3D12Resource* resource, D3D12_RESOURCE_STATES state);`

`/**`

`* Remove a resource from the global resource state array (map).`

`* This should only be done when the resource is destroyed.`

`*/`

`static` `void RemoveGlobalResourceState(ID3D12Resource* resource);`

The  `AddGlobalResourceState`  method is used to register a resoruce and its initial state with the  _global resource state map_. This is done whenever a new resource is created. Just before a resource is destroyed, the  `RemoveGlobalResourceState`  can be used to remove the resource from the  _global resource state map_.

When using  `[ComPtr](https://docs.microsoft.com/en-us/cpp/windows/comptr-class)`s it is often difficult (or impossible) to know when a resource is about to be released. For this reason, resources are stored as raw pointers in the  _global resource state map_  and their ref counter is not increased and won't prevent the resource from being released. Although the  [Windows Runtime Library](https://docs.microsoft.com/en-us/cpp/windows/wrl-reference)  provides a  `[WeakRef](https://docs.microsoft.com/en-us/cpp/windows/weakref-class)`  class, its usage seems unintuitive and did not add much value for this use case (since having dangling pointers in the  _global resource state map_  does not cause any problems).  

ResourceStateTracker.h

152

153

154

`private``:`

`// An array (vector) of resource barriers.`

`using` `ResourceBarriers = std::vector<D3D12_RESOURCE_BARRIER>;`

`ResourceBarriers`  is a type alias for a  `[vector](https://en.cppreference.com/w/cpp/container/vector)`  array of  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`s.

ResourceStateTracker.h

156

157

158

159

160

161

162

`// Pending resource transitions are committed before a command list`

`// is executed on the command queue. This guarantees that resources will`

`// be in the expected state at the beginning of a command list.`

`ResourceBarriers m_PendingResourceBarriers;`

`// Resource barriers that need to be committed to the command list.`

`ResourceBarriers m_ResourceBarriers;`

The  `m_PendingResourceBarriers`  member variable is used to store  _pending_  resource barriers and the  `m_ResourceBarriers`  member variable is used to store  _non-pending_resource barriers.

The  `ResourceState`  struct is an internal struct that is used to track the state of the  _subresources_  of a resource.

ResourceStateTracker.h

164

165

166

167

168

169

170

`// Tracks the state of a particular resource and all of its subresources.`

`struct` `ResourceState`

`{`

`// Initialize all of the subresources within a resource to the given state.`

`explicit` `ResourceState(D3D12_RESOURCE_STATES state = D3D12_RESOURCE_STATE_COMMON)`

`: State(state)`

`{}`

The  `ResourceState`  struct is used by the  `ResourceStateTracker`  to track the state of a resource and all of its subresources. By default, a resource (and all of its subresources) is initialized to the  `[D3D12_RESOURCE_STATE_COMMON](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state.

ResourceStateTracker.h

172

173

174

175

176

177

178

179

180

181

182

183

184

`// Set a subresource to a particular state.`

`void SetSubresourceState(``UINT` `subresource, D3D12_RESOURCE_STATES state)`

`{`

`if` `(subresource == D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES)`

`{`

`State = state;`

`SubresourceState.clear();`

`}`

`else`

`{`

`SubresourceState[subresource] = state;`

`}`

`}`

The  `ResourceState::SetSubresourceState`  method is used to set the state of a (sub)resource. If  `[D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_transition_barrier)`  is specified as the subresource index, then the state of the entire resource is updated and the  `SubresourceState`  map (defined later) is cleared. Otherwise, the subresource index is used to update the state of the subresource within the  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  on line 182.

ResourceStateTracker.h

186

187

188

189

190

191

192

193

194

195

196

197

198

199

`// Get the state of a (sub)resource within the resource.`

`// If the specified subresource is not found in the SubresourceState array (map)`

`// then the state of the resource (D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES) is`

`// returned.`

`D3D12_RESOURCE_STATES GetSubresourceState(``UINT` `subresource)` `const`

`{`

`D3D12_RESOURCE_STATES state = State;`

`const` `auto iter = SubresourceState.find(subresource);`

`if` `(iter != SubresourceState.end())`

`{`

`state = iter->second;`

`}`

`return` `state;`

`}`

The  `ResourceState::GetSubresourceState`  method is used to query the state of the (sub)resource. If the subresource index is not found in the  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`, the state of the entire resource (`State`) is returned.

ResourceStateTracker.h

201

202

203

204

205

`// If the SubresourceState array (map) is empty, then the State variable defines`

`// the state of all of the subresources.`

`D3D12_RESOURCE_STATES State;`

`std::map<``UINT``, D3D12_RESOURCE_STATES> SubresourceState;`

`};`

The  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  is used to store the current state of a subresource. If the  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  is empty, then the resource and all of its subresources are in the state defined by the  `State`  variable.

ResourceStateTracker.h

207

`using` `ResourceStateMap = std::unordered_map<ID3D12Resource*, ResourceState>;`

`ResourceStateMap`  is a type alias of a  `[std::unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map)`  which maps a resource (pointer) to its  `ResourceState`.

ResourceStateTracker.h

209

210

211

212

`// The final (last known state) of the resources within a command list.`

`// The final resource state is committed to the global resource state when the`

`// command list is closed but before it is executed on the command queue.`

`ResourceStateMap m_FinalResourceState;`

The  `m_FinalResourceState`  member variable stores the final known state of a resource in the  `ResourceStateTracker`.

ResourceStateTracker.h

214

215

216

`// The global resource state array (map) stores the state of a resource`

`// between command list execution.`

`static` `ResourceStateMap ms_GlobalResourceState;`

The  `ms_GlobalResourceState`  static member variable is used to store the global state of a resource. The  **global resource state map**  is updated whenever a command list is closed (just before it is executed on the command queue).

ResourceStateTracker.h

218

219

220

221

`// The mutex protects shared access to the GlobalResourceState map.`

`static` `std::mutex ms_GlobalMutex;`

`static` `bool` `ms_IsLocked;`

`};`

The  `ms_GlobalMutex`  and  `ms_IsLocked`  static member variables are used to synchronize access to the  _global resource state map_  across multiple threads.

[![Resource State Tracker Header File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for ResourceStateTracker.h](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/inc/ResourceStateTracker.h)

### RESOURCESTATETRACKER PREAMBLE

Besides the header file for the  `ResourceStateTracker`  class, several other header files are included in the implementation file.

ResourceStateTracker.cpp

1

2

3

4

5

6

`#include <DX12LibPCH.h>`

`#include <ResourceStateTracker.h>`

`#include <CommandList.h>`

`#include <Resource.h>`

The  `DX12LibPCH.h`  header file is the precompiled header file for the DX12Lib project.

The  `ResourceStateTracker.h`  header file contains the declaration for the  `ResourceStateTracker`  class. This header file is described in the previous section.

The  `CommandList`  and  `Resource`  classes were only forward-declared in the  `ResourceStateTracker.h`  header file their headers are included here so the  `ResourceStateTracker`  can use those classes.

ResourceStateTracker.cpp

8

9

10

11

`// Static definitions.`

`std::mutex ResourceStateTracker::ms_GlobalMutex;`

`bool` `ResourceStateTracker::ms_IsLocked =` `false``;`

`ResourceStateTracker::ResourceStateMap ResourceStateTracker::ms_GlobalResourceState;`

Static member variables that are declared in the header file need to be defined to allocate space for them in static memory.

### RESOURCESTATETRACKER::RESOURCEBARRIER

The  `ResourceBarrier`  method is used to add a resource barrier to the  `ResourceStateTracker`.

ResourceStateTracker.cpp

19

20

`void ResourceStateTracker::ResourceBarrier(``const` `D3D12_RESOURCE_BARRIER& barrier)`

`{`

The  `ResourceBarrier`  method takes a single  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`  as its only argument.

ResourceStateTracker.cpp

21

22

23

`if` `(barrier.Type == D3D12_RESOURCE_BARRIER_TYPE_TRANSITION)`

`{`

`const` `D3D12_RESOURCE_TRANSITION_BARRIER& transitionBarrier = barrier.Transition;`

Since only  _transition_  barriers need to resove the  _before_  state of the resource, transition barriers are handled seperatly from UAV or alias barriers.

On line 23, the  `[D3D12_RESOURCE_TRANSITION_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_transition_barrier)`  is queried from the  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`  structure.

ResourceStateTracker.cpp

25

26

27

28

29

30

`// First check if there is already a known "final" state for the given resource.`

`// If there is, the resource has been used on the command list before and`

`// already has a known state within the command list execution.`

`const` `auto iter = m_FinalResourceState.find(transitionBarrier.pResource);`

`if` `(iter != m_FinalResourceState.end())`

`{`

If the resource has been used on the command list before, then its previous state is known by the  `ResourceStateTracker`  and that state is stored in the  `m_FinalResourceState`  map.

ResourceStateTracker.cpp

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

`auto& resourceState = iter->second;`

`// If the known final state of the resource is different...`

`if` `( transitionBarrier.Subresource == D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES &&`

`!resourceState.SubresourceState.empty() )`

`{`

`// First transition all of the subresources if they are different than the StateAfter.`

`for` `( auto subresourceState : resourceState.SubresourceState )`

`{`

`if` `( transitionBarrier.StateAfter != subresourceState.second )`

`{`

`D3D12_RESOURCE_BARRIER newBarrier = barrier;`

`newBarrier.Transition.Subresource = subresourceState.first;`

`newBarrier.Transition.StateBefore = subresourceState.second;`

`m_ResourceBarriers.push_back( newBarrier );`

`}`

`}`

`}`

The iterator that is retrieved on line 28 stores the  `ResourceState`  struct of the resource. The  `ResourceState`  struct contains a  `[map](https://en.cppreference.com/w/cpp/container/map)`  of subresource states. If the transition barrier is transitioning all subresources (`D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES`)  _and_  there are subresources that are in a  _different_  state then a transition barrier for each subresource that is not in the correct state is added to the  `m_ResourceBarriers`  array.

ResourceStateTracker.cpp

48

49

50

51

52

53

54

55

56

57

58

`else`

`{`

`auto finalState = resourceState.GetSubresourceState( transitionBarrier.Subresource );`

`if` `( transitionBarrier.StateAfter != finalState )`

`{`

`// Push a new transition barrier with the correct before state.`

`D3D12_RESOURCE_BARRIER newBarrier = barrier;`

`newBarrier.Transition.StateBefore = finalState;`

`m_ResourceBarriers.push_back( newBarrier );`

`}`

`}`

Else, if the transition barrier is transitioning only a single subresource, or all subresources are in the same state (the  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  is empty) and the current (final) state of the (sub)resource is different than the requested state, then a single transition barrier is added to the  `m_ResourceBarriers`  array on line 56.

ResourceStateTracker.cpp

60

61

62

63

64

65

`else` `// In this case, the resource is being used on the command list for the first time.`

`{`

`// Add a pending barrier. The pending barriers will be resolved`

`// before the command list is executed on the command queue.`

`m_PendingResourceBarriers.push_back(barrier);`

`}`

If the resource is being used on the command list for the first time (the resource was not found in the  `m_FinalResourceState`  map) then the resource barrier is added to the  `m_PendingResourceBarriers`  array and the  _before_  state will be resolved later (before the command list is executed on the command queue).

ResourceStateTracker.cpp

67

68

69

`// Push the final known state (possibly replacing the previously known state for the subresource).`

`m_FinalResourceState[transitionBarrier.pResource].SetSubresourceState(transitionBarrier.Subresource, transitionBarrier.StateAfter);`

`}`

Whether the resource has been seen on the command list before or not, its final state is added to the  `m_FinalResourceState`  map, possibly replacing the previously known state of the (sub)resource.

ResourceStateTracker.cpp

70

71

72

73

74

75

`else`

`{`

`// Just push non-transition barriers to the resource barriers array.`

`m_ResourceBarriers.push_back(barrier);`

`}`

`}`

UAV and aliasing barriers (`[D3D12_RESOURCE_BARRIER_TYPE_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`, and  `[D3D12_RESOURCE_BARRIER_TYPE_ALIASING](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`) do not require any special treatment and are simply pushed to the back of the  `m_ResourceBarriers`  array.

### RESOURCESTATETRACKER::TRANSITIONRESOURCE

The  `TransitionResource`  method is simply a helper method to forward a transition barrier to the  `[ResourceBarrier](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerResourceBarrier)`  method described above.

ResourceStateTracker.cpp

77

78

79

80

81

82

83

84

85

86

87

88

`void ResourceStateTracker::TransitionResource( ID3D12Resource* resource, D3D12_RESOURCE_STATES stateAfter,` `UINT` `subResource )`

`{`

`if` `( resource )`

`{`

`ResourceBarrier( CD3DX12_RESOURCE_BARRIER::Transition( resource, D3D12_RESOURCE_STATE_COMMON, stateAfter, subResource ) );`

`}`

`}`

`void ResourceStateTracker::TransitionResource(` `const` `Resource& resource, D3D12_RESOURCE_STATES stateAfter,` `UINT` `subResource )`

`{`

`TransitionResource( resource.GetD3D12Resource().Get(), stateAfter, subResource );`

`}`

There are two versions of the  `TransitionResource`  method shown here. One that takes a  _raw pointer_  to a  `[ID3D12Resource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12resource)`  and the other takes a  _const reference_  to a  `Resource`object (which is a type provided by the DX12Lib framework project). The  `Resource`class simply provides a wrapper for a  `[ID3D12Resource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12resource)`  and it also serves as the base class for other resource types in the DX12Lib framwork.

### RESOURCESTATETRACKER::UAVBARRIER

The  `UAVBarrier`  method is used to add a  `[D3D12_RESOURCE_BARRIER_TYPE_UAV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`  typed  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`  to the command list.

ResourceStateTracker.cpp

90

91

92

93

94

95

`void ResourceStateTracker::UAVBarrier(``const` `Resource* resource )`

`{`

`ID3D12Resource* pResource = resource != nullptr ? resource->GetD3D12Resource().Get() : nullptr;`

`ResourceBarrier(CD3DX12_RESOURCE_BARRIER::UAV(pResource));`

`}`

When submitting a UAV barrier to a command list, the specified resource can be null. If the specified resource is null, then all UAV operations must complete before any UAV operation can be performed. This can cause pipeline stalls and should be avoided. UAV barriers should only be used to synchronize read/write operations on the same UAV resource.

### RESOURCESTATETRACKER::ALIASBARRIER

The  `AliasBarrier`  barrier method is used to add a  `[D3D12_RESOURCE_BARRIER_TYPE_ALIASING](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`  typed  `[D3D12_RESOURCE_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_barrier)`  to the command list.

ResourceStateTracker.cpp

97

98

99

100

101

102

103

`void ResourceStateTracker::AliasBarrier(``const` `Resource* resourceBefore,` `const` `Resource* resourceAfter)`

`{`

`ID3D12Resource* pResourceBefore = resourceBefore != nullptr ? resourceBefore->GetD3D12Resource().Get() : nullptr;`

`ID3D12Resource* pResourceAfter = resourceAfter != nullptr ? resourceAfter->GetD3D12Resource().Get() : nullptr;`

`ResourceBarrier(CD3DX12_RESOURCE_BARRIER::Aliasing(pResourceBefore, pResourceAfter));`

`}`

Aliasing barriers are used to transition two resources that have mappings into the same heap. This is commonly used with  _placed_  or  _reserved_  resources that have overlapping mappings into the same heap. One or both resources can be null which indicates that accessing any placed or reserved resource could cause aliasing.

### RESOURCESTATETRACKER::FLUSHRESOURCEBARRIERS

The  `FlushResourceBarriers`  method is used to push the  _non-pending_  resource barriers to the specified command list.

ResourceStateTracker.cpp

105

106

107

108

109

110

111

112

113

114

`void ResourceStateTracker::FlushResourceBarriers(CommandList& commandList)`

`{`

`UINT` `numBarriers =` `static_cast``<``UINT``>(m_ResourceBarriers.size());`

`if` `(numBarriers > 0 )`

`{`

`auto d3d12CommandList = commandList.GetGraphicsCommandList();`

`d3d12CommandList->ResourceBarrier(numBarriers, m_ResourceBarriers.data());`

`m_ResourceBarriers.clear();`

`}`

`}`

The  `FlushResourceBarriers`  method is straightforward. It simply checks if the  `m_ResourceBarriers`  array contains any barriers. If so, the resource barriers are added to the command list using the  `[ID3D12GraphicsCommandList::ResourceBarrier](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-resourcebarrier)`  method.

After adding the resource barriers to the command list, the  `m_ResourceBarriers`  (vector) array is cleared.

### RESOURCESTATETRACKER::FLUSHPENDINGRESOURCEBARRIERS

The  `FlushPendingResourceBarriers`  method is not so straightforward as the  `FlushResourceBarriers`  method. This method adds only the resource barriers that are required to transition the resources into the correct state required by the command list. The  `FlushPendingResourceBarriers`  method adds the transition barriers to the intermediate command list (C) depicted in the  [image above](https://www.3dgep.com/learning-directx12-3/#attachment_8874). In order to determine if a pending transition needs to be added to the intermediate command list, its  _global_  state is compared against the  _pending_  state. If the  _pending_  state is different than the  _global_state, then a transition barrier is added to the intermediate command list.

ResourceStateTracker.cpp

116

117

118

119

120

121

122

123

124

125

`uint32_t` `ResourceStateTracker::FlushPendingResourceBarriers(CommandList& commandList)`

`{`

`assert``(ms_IsLocked);`

`// Resolve the pending resource barriers by checking the global state of the`

`// (sub)resources. Add barriers if the pending state and the global state do`

`// not match.`

`ResourceBarriers resourceBarriers;`

`// Reserve enough space (worst-case, all pending barriers).`

`resourceBarriers.reserve(m_PendingResourceBarriers.size());`

In order to gurantee the consistency of the  _global_  resource state map, access to the global map must be exclusive to the current thread. If access to the global resource state map is not locked, the assert on line 118 fails.

The  `resourceBarriers`  local variable is a vector that is used to add any pending resource barriers to the command list. The size of the  `resourceBarriers`  (vector) array will be (at most) the size of the  `m_PendingResourceBarriers`  (vector) array. As an optimization, the worst-case size for the  `resourceBarriers`  (vector) array is pre-allocated on line 125.

ResourceStateTracker.cpp

127

128

129

130

131

`for` `(auto pendingBarrier : m_PendingResourceBarriers)`

`{`

`if` `(pendingBarrier.Type == D3D12_RESOURCE_BARRIER_TYPE_TRANSITION)` `// Only transition barriers should be pending...`

`{`

`auto pendingTransition = pendingBarrier.Transition;`

Only pending resource barriers of type  `[D3D12_RESOURCE_BARRIER_TYPE_TRANSITION](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`  need to be checked (in fact, the  `m_PendingResourceBarriers`  array should only contain  _transition_  barriers) and UAV and alias barriers are ignored.

On line 131, the  `[D3D12_RESOURCE_TRANSITION_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_barrier_type)`  structure is retrieved from the pending resource barrier.

ResourceStateTracker.cpp

133

134

135

`const` `auto& iter = ms_GlobalResourceState.find(pendingTransition.pResource);`

`if` `(iter != ms_GlobalResourceState.end())`

`{`

The globally known state of the resource is queried from the  `ms_GlobalResourceState`state array.

ResourceStateTracker.cpp

136

137

138

139

140

141

142

143

144

145

146

147

148

149

150

151

152

153

`// If all subresources are being transitioned, and there are multiple`

`// subresources of the resource that are in a different state...`

`auto& resourceState = iter->second;`

`if` `( pendingTransition.Subresource == D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES &&`

`!resourceState.SubresourceState.empty() )`

`{`

`// Transition all subresources`

`for` `( auto subresourceState : resourceState.SubresourceState )`

`{`

`if` `( pendingTransition.StateAfter != subresourceState.second )`

`{`

`D3D12_RESOURCE_BARRIER newBarrier = pendingBarrier;`

`newBarrier.Transition.Subresource = subresourceState.first;`

`newBarrier.Transition.StateBefore = subresourceState.second;`

`resourceBarriers.push_back( newBarrier );`

`}`

`}`

`}`

If the pending resource barrier is transitioning  _all_  subresources (`D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES`)  _and_  there are some subresources that are in a different state (the  `SubresourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  is not empty) then every subresource that is in a different state needs an explicit transition to the correct state.

ResourceStateTracker.cpp

154

155

156

157

158

159

160

161

162

163

164

`else`

`{`

`// No (sub)resources need to be transitioned. Just add a single transition barrier (if needed).`

`auto globalState = ( iter->second ).GetSubresourceState( pendingTransition.Subresource );`

`if` `( pendingTransition.StateAfter != globalState )`

`{`

`// Fix-up the before state based on current global state of the resource.`

`pendingBarrier.Transition.StateBefore = globalState;`

`resourceBarriers.push_back( pendingBarrier );`

`}`

`}`

Otherwise either only a single subresource is being transitioned or there are no subresources that are in a different state, then only a single transition barrier is required. If the (sub)resource is not in the correct  _after_  state (according to its  _global_  state), then a transition barrier is added to the  `resourceBarriers`  array. The current  _global_  state of the resource is used to  _fix-up_  the  _before_  state of the transition barrier.

ResourceStateTracker.cpp

165

166

167

168

169

170

171

172

173

174

175

176

177

178

179

`}`

`}`

`}`

`UINT` `numBarriers =` `static_cast``<``UINT``>(resourceBarriers.size());`

`if` `(numBarriers > 0 )`

`{`

`auto d3d12CommandList = commandList.GetGraphicsCommandList();`

`d3d12CommandList->ResourceBarrier(numBarriers, resourceBarriers.data());`

`}`

`m_PendingResourceBarriers.clear();`

`return` `numBarriers;`

`}`

And finally, the resource barriers (if any) are added to the (intermediate) command list on line 173.

After comitting all of the pending resource barriers to the command list, the  `m_PendingResourceBarriers`  (vector) array is cleared.

The number of barriers (`numBarriers`) that were generated is returned to the calling function. If the number of resource barriers is 0, then there is no need to execute the intermediate command list on the command queue.

### RESOURCESTATETRACKER::COMMITFINALRESOURCESTATES

The purpose of the  `CommitFinalResourceStates`  method is to ensure that the  _final_  state of the resource is committed to the static  _global_  state map.

ResourceStateTracker.cpp

181

182

183

184

185

186

187

188

189

190

191

192

`void ResourceStateTracker::CommitFinalResourceStates()`

`{`

`assert``(ms_IsLocked);`

`// Commit final resource states to the global resource state array (map).`

`for` `(``const` `auto& resourceState : m_FinalResourceState)`

`{`

`ms_GlobalResourceState[resourceState.first] = resourceState.second;`

`}`

`m_FinalResourceState.clear();`

`}`

The  `CommitFinalResourceStates`  method simply merges the entries of the  `m_FinalResourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`  with the  `ms_GlobalResourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`. After merging the final state of the resources into the global state map, the final state map is cleared on line 191.

### RESOURCESTATETRACKER::RESET

The  `ResourceStateTracker`  is reset whenver the command list that owns the  `ResourceStateTracker`  is reset.

ResourceStateTracker.cpp

1

2

3

4

5

6

7

`void ResourceStateTracker::Reset()`

`{`

`// Reset the pending, current, and final resource states.`

`m_PendingResourceBarriers.clear();`

`m_ResourceBarriers.clear();`

`m_FinalResourceState.clear();`

`}`

The  `Reset`  method simply clears the  `m_PendingResourceBarriers`,  `m_ResourceBarriers`(`[vector](https://en.cppreference.com/w/cpp/container/vector)`) arrays, and the  `m_FinalResourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`.

If the  `ResourceStateTracker`  is used correctly, then the calling the  `Reset`method should be superfluous.  

### RESOURCESTATETRACKER::LOCK

The  `Lock`  (static) method is used to lock the mutex which ensures only the current thread has access to the  `ms_GlobalResourceState`  array.

ResourceStateTracker.cpp

202

203

204

205

206

`void ResourceStateTracker::Lock()`

`{`

`ms_GlobalMutex.lock();`

`ms_IsLocked =` `true``;`

`}`

### RESOURCESTATETRACKER::UNLOCK

Similar to the  `Lock`  method, the  `Unlock`  method unlocks the global mutex.

ResourceStateTracker.cpp

208

209

210

211

212

`void ResourceStateTracker::Unlock()`

`{`

`ms_IsLocked =` `false``;`

`ms_GlobalMutex.unlock();`

`}`

### RESOURCESTATETRACKER::ADDGLOBALRESOURCESTATE

The  `AddGlobalResourceState`  method is used whenever a new resource is created using  `[ID3D12Device::CreateCommittedResource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-createcommittedresource)`,  `[ID3D12Device::CreatePlacedResource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-createplacedresource)`, or  `[ID3D12Device::CreateReservedResource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12device-createreservedresource)`.

ResourceStateTracker.cpp

214

215

216

217

218

219

220

221

`void ResourceStateTracker::AddGlobalResourceState(ID3D12Resource* resource, D3D12_RESOURCE_STATES state)`

`{`

`if` `( resource != nullptr )`

`{`

`std::lock_guard<std::mutex> lock(ms_GlobalMutex);`

`ms_GlobalResourceState[resource].SetSubresourceState(D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES, state);`

`}`

`}`

The resource and the initial resource state is added to the  `ms_GlobalResourceState``[map](https://en.cppreference.com/w/cpp/container/map)`  on line 219.

### RESOURCESTATETRACKER::REMOVEGLOBALRESOURCESTATE

Similar to the  `AddGlobalResourceState`, the  `RemoveGlobalResourceState`  removes the resource from the  `ms_GlobalResourceState`  `[map](https://en.cppreference.com/w/cpp/container/map)`.

ResourceStateTracker.cpp

223

224

225

226

227

228

229

230

`void ResourceStateTracker::RemoveGlobalResourceState(ID3D12Resource* resource)`

`{`

`if` `( resource != nullptr )`

`{`

`std::lock_guard<std::mutex> lock(ms_GlobalMutex);`

`ms_GlobalResourceState.erase(resource);`

`}`

`}`

[![Resource State Tracker Source File](https://www.3dgep.com/wp-content/uploads/2017/12/GitHub-Mark-120px-plus.png)View the full source code for ResourceStateTracker.cpp](https://github.com/jpvanoosten/LearningDirectX12/blob/v0.0.3/DX12Lib/src/ResourceStateTracker.cpp)

# Custom Command List

In order to provide a simple interface to the end user for the  `[UploadBuffer](https://www.3dgep.com/learning-directx12-3/#Upload_Buffer)`,  `[DescriptorAllocator](https://www.3dgep.com/learning-directx12-3/#Descriptor_Allocator)`,  `[DynamicDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)`, and the  `[ResourceStateTracker](https://www.3dgep.com/learning-directx12-3/#Resource_State_Tracking)`  classes described in this article, the DX12Lib project provides a custom  `CommandList`  class. The  `CommandList`  class is one of the largest classes in the DX12Lib project and won't be described in complete detail in this article. Only the methods of the  `CommandList`  class that utialize one of the classes described here are shown.

## CommandList Class

The  `CommandList`  class is a wrapper for the  `[ID3D12GraphicsCommandList](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12graphicscommandlist)`  type. Almost all of the command list functionality that is required for the DirectX 12 tutorials in this series is implemented in the custom  `CommandList`  class and there should be little to no reason to access the underlying  `[ID3D12GraphicsCommandList](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nn-d3d12-id3d12graphicscommandlist)`. The custom  `CommandList`  class handles resource barriers, copying (CPU and GPU) resources, texture loading, mipmap generation (mipmap generation is explained in a later lesson), binding resources to the pipeline, descriptor heaps, draw, and dispatch commands.

### COMMANDLIST::TRANSITIONBARRIER

The  `TransitionBarrier`  method is used to forward a  `[D3D12_RESOURCE_TRANSITION_BARRIER](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_resource_transition_barrier)`  structure to the  `[ResourceStateTracker::ResourceBarrier](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerResourceBarrier)`  method.

CommandList.cpp

49

50

51

52

53

54

55

56

57

58

59

60

61

62

63

`void CommandList::TransitionBarrier(` `const` `Resource& resource, D3D12_RESOURCE_STATES stateAfter,` `UINT` `subResource,` `bool` `flushBarriers )`

`{`

`auto d3d12Resource = resource.GetD3D12Resource();`

`if` `( d3d12Resource )`

`{`

`// The "before" state is not important. It will be resolved by the resource state tracker.`

`auto barrier = CD3DX12_RESOURCE_BARRIER::Transition( d3d12Resource.Get(), D3D12_RESOURCE_STATE_COMMON, stateAfter, subResource );`

`m_ResourceStateTracker->ResourceBarrier( barrier );`

`}`

`if` `( flushBarriers )`

`{`

`FlushResourceBarriers();`

`}`

`}`

The  `TransitionBarrier`  method takes a  _const reference_  to a  `Resource`, the  `[D3D12_RESOURCE_STATES](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`, the subresource to transition (which defaults to  `D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES`), and a boolean indicating if the resource barriers should be flushed to the command list as arguments to the method.

It is interesting to note that the  `TransitionBarrier`  method does not need the  _before state_  of the resource since the  `ResourceStateTracker`  will resolve the before state when comitting the resource barriers.

If the resource barriers should be committed to the command list, then the  `FlushResourceBarriers`  method is used which in-turn calls the  `[ResourceStateTracker::FlushResourceBarriers](https://www.3dgep.com/learning-directx12-3/#ResourceStateTrackerFlushResourceBarriers)`  method.

There are also  `CommandList::UAVBarrier`  and  `CommandList::AliasingBarrier`  methods that add resource barriers of those types to the  `ResourceStateTracker`. The description of those methods is not shown here for brevity.

### COMMANDLIST::COPYRESOURCE

The  `CopyResource`  is used to copy one GPU resource to another (copying of resources is a common operation in rendering pipelines). This method is shown here since it provides a good example of transitioning resources to the correct state before performing an operation that requires the resources to be in a specific state.

CommandList.cpp

97

98

99

100

101

102

103

104

105

106

107

108

`void CommandList::CopyResource( Resource& dstRes,` `const` `Resource& srcRes )`

`{`

`TransitionBarrier( dstRes, D3D12_RESOURCE_STATE_COPY_DEST );`

`TransitionBarrier( srcRes, D3D12_RESOURCE_STATE_COPY_SOURCE );`

`FlushResourceBarriers();`

`m_d3d12CommandList->CopyResource( dstRes.GetD3D12Resource().Get(), srcRes.GetD3D12Resource().Get() );`

`TrackResource(dstRes);`

`TrackResource(srcRes);`

`}`

Before copying the contents of one resource to another, the destination needs to be in the  `[D3D12_RESOURCE_STATE_COPY_DEST](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state and the source resource needs to be in the  `[D3D12_RESOURCE_STATE_COPY_SOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state. The resources are transitioned to the correct state on lines 99-100. Before issuing the  `[ID3D12GraphicsCommandList::CopyResource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-copyresource)`method, the resource barriers need to be comitted to the command list. This is accomplished using the  `FlushResourceBarriers`  method.

On line 104, the source resource is copied to the destination resource using the  `[ID3D12GraphicsCommandList::CopyResource](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-copyresource)`  method.

To ensure neither the source nor the destination resources go out of scope while the resource is still being referenced by the command list, the resources are added to a list of  _tracked_  objects using the  `TrackResource`  method on lines 106-107. Using the  `TrackResource`  method, short lived (temporary) resoruces can be used on a command list without having to track their lifetime outside of the command list. This is useful for generating mipmaps on texture resources when the original texture resource doesn't support UAV writes, a temporary resource object is created which supports UAV writes. The temporary resource will stay in scope until the command list is reset (when it is finished executing on the command queue).

### COMMANDLIST::SETGRAPHICSDYNAMICCONSTANTBUFFER

The  `SetGraphicsDynamicConstantBuffer`  method uses the  `[UploadBuffer](https://www.3dgep.com/learning-directx12-3/#Upload_Buffer)`  class to update a constant buffer that needs to change often (for example, the  _world matrix_  for a model that is changed for every model drawn). For smaller constant buffers (less than 16 32-bit constants) the  `[ID3D12GraphicsCommandList::SetGraphicsRoot32BitConstants](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setgraphicsroot32bitconstants)`method can also be used to update dynamic constatnt buffer data, but for larger constant buffers, it is probably better to use an upload heap.

CommandList.cpp

782

783

784

785

786

787

788

789

`void CommandList::SetGraphicsDynamicConstantBuffer(` `uint32_t` `rootParameterIndex,` `size_t` `sizeInBytes,` `const` `void* bufferData )`

`{`

`// Constant buffers must be 256-byte aligned.`

`auto heapAllococation = m_UploadBuffer->Allocate( sizeInBytes, D3D12_CONSTANT_BUFFER_DATA_PLACEMENT_ALIGNMENT );`

`memcpy``( heapAllococation.CPU, bufferData, sizeInBytes );`

`m_d3d12CommandList->SetGraphicsRootConstantBufferView( rootParameterIndex, heapAllococation.GPU );`

`}`

The  `SetGraphicsDynamicConstantBuffer`  method takes the root parameter index, the size of the constant buffer, and a pointer to the constant buffer data in host (CPU) memory as arguments to the method.

On line 785, an allocation for the requested size and required alignment (constant buffers are required to be aligned to 256 bytes) is made using the  `[UploadBuffer::Allocate](https://www.3dgep.com/learning-directx12-3/#UploadBufferAllocate)`  method. This method returns a  `UploadBuffer::Allocation`struct which just contains the CPU and GPU pointers to the memory in the upload heap.

The buffer data is copied to the upload heap using a simple  `[memcpy](https://en.cppreference.com/w/c/string/byte/memcpy)`  function on line 786.

The location of the data in GPU memory is then set using the  `[ID3D12GraphicsCommandList::SetGraphicsRootConstantBufferView](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-setgraphicsrootconstantbufferview)`  method.

The root parameter at index  `rootParameterIndex`  must be set to  `[D3D12_ROOT_PARAMETER_TYPE_CBV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_root_parameter_type)`  to use the  `SetGraphicsDynamicConstantBuffer`  method described here.  

### COMMANDLIST::SETSHADERRESOURCEVIEW

The  `SetShaderResourceView`  method uses the  `[DynamicDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)`  class to stage an SRV to a GPU visible descriptor heap. This method also transitions the resource to the correct state for use as an SRV on the graphics or compute pipelines.

CommandList.cpp

931

932

933

934

935

936

937

938

939

940

941

942

943

944

945

946

947

948

949

950

951

952

953

954

`void CommandList::SetShaderResourceView(` `uint32_t` `rootParameterIndex,`

`uint32_t` `descriptorOffset,`

`const` `Resource& resource,`

`D3D12_RESOURCE_STATES stateAfter,`

`UINT` `firstSubresource,`

`UINT` `numSubresources,`

`const` `D3D12_SHADER_RESOURCE_VIEW_DESC* srv)`

`{`

`if` `(numSubresources < D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES)`

`{`

`for` `(``uint32_t` `i = 0; i < numSubresources; ++i)`

`{`

`TransitionBarrier(resource, stateAfter, firstSubresource + i);`

`}`

`}`

`else`

`{`

`TransitionBarrier(resource, stateAfter);`

`}`

`m_DynamicDescriptorHeap[D3D12_DESCRIPTOR_HEAP_TYPE_CBV_SRV_UAV]->StageDescriptors( rootParameterIndex, descriptorOffset, 1, resource.GetShaderResourceView( srv ) );`

`TrackResource(resource);`

`}`

As can be seen from the code snippet above, the  `SetShaderResourceView`  method takes a lot of arguments:

-   `uint32_t rootParameterIndex`: The root parameter index to assign the SRV to. The root parameter must be of type  `[D3D12_ROOT_PARAMETER_TYPE_DESCRIPTOR_TABLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_root_parameter_type)`  and the  `descriptorOffset`  must refer to a descriptor in a  `[D3D12_DESCRIPTOR_RANGE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_descriptor_range)`  of type  `[D3D12_DESCRIPTOR_RANGE_TYPE_SRV](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_descriptor_range_type)`.
-   `uint32_t descriptorOffset`: The offset starting from the first descriptor in the  `[D3D12_ROOT_DESCRIPTOR_TABLE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_root_descriptor_table).`
-   `const Resource& resource`: The  `Resource`  to bind.
-   `[D3D12_RESOURCE_STATES](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states) stateAfter`: The required state of the resource. If the resource is being bound for reading in a pixel shader, it should be transitioned to the  `[D3D12_RESOURCE_STATE_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state, otherwise it should be transitioned to the  `[D3D12_RESOURCE_STATE_NON_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`  state. The default value for this argument is  `[D3D12_RESOURCE_STATE_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)|[D3D12_RESOURCE_STATE_NON_PIXEL_SHADER_RESOURCE](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ne-d3d12-d3d12_resource_states)`which allows the resource to be used in either a pixel shader or a non-pixel shader (but it may not be optimal to rely on the combined state).
-   `UINT firstSubresource`: The first subresource to transition to the requested state. The default value for this argument is 0.
-   `UINT numSubresources`: The number of subresoruces to transition. The default value for this argument is  `D3D12_RESOURCE_BARRIER_ALL_SUBRESOURCES`.
-   `const [D3D12_SHADER_RESOURCE_VIEW_DESC](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/ns-d3d12-d3d12_shader_resource_view_desc)* srv`: The SRV description to use for the resource in the shader. By default, this value is  `nullptr`  which uses the default SRV for the resource. It is necessary to specify the SRV description for the resource when a depth buffer resource needs to be read in a pixel shader (for example, when performing shadow mapping).

On lines 939-949 of the  `SetShaderResourceView`  method, the subresources are transitioned to the reqeusted state using the  `[TransitionBarrier](https://www.3dgep.com/learning-directx12-3/#CommandListTransitionBarrier)`  method described earlier.

The SRV matching the SRV description is retrieved from the resource using the  `Resource::GetShaderResourceView`  method (not shown here) and staged to the  `[DynamicDescriptorHeap](https://www.3dgep.com/learning-directx12-3/#Dynamic_Descriptor_Heap)`  using the  `[DynamicDescriptorHeap::StageDescriptors](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapStageDescriptors)`  described earlier.

To ensure the lifetime of the resource, it is added to a list of tracked resources using the  `TrackResource`  method on line 953.

There is also a similar  `SetUnorderedAccessView`  method which performs the same function for UAVs as the  `SetShaderResourceView`  does for SRVs. The  `SetUnorderedAccessView`  method is not described here for brevity.

### COMMANDLIST::DRAW

The  `Draw`  method is used to render geometry to the currently bound render target. Before executing a  `Draw`  command on the command list, all resource barriers must be flushed to the command list using the  `FlushResourceBarriers`  method and any resource descriptors that were staged to the  `DynamicDescriptorHeap`  need to be committed.

CommandList.cpp

1020

1021

1022

1023

1024

1025

1026

1027

1028

1029

1030

`void CommandList::Draw(` `uint32_t` `vertexCount,` `uint32_t` `instanceCount,` `uint32_t` `startVertex,` `uint32_t` `startInstance )`

`{`

`FlushResourceBarriers();`

`for` `(` `int` `i = 0; i < D3D12_DESCRIPTOR_HEAP_TYPE_NUM_TYPES; ++i )`

`{`

`m_DynamicDescriptorHeap[i]->CommitStagedDescriptorsForDraw( *``this` `);`

`}`

`m_d3d12CommandList->DrawInstanced( vertexCount, instanceCount, startVertex, startInstance );`

`}`

The  `Draw`  method takes the same parameters as the  `[ID3D12GraphicsCommandList::DrawInstanced](https://docs.microsoft.com/en-us/windows/desktop/api/d3d12/nf-d3d12-id3d12graphicscommandlist-drawinstanced)`  method. Since this method was already described in the  [previous article](https://www.3dgep.com/learning-directx12-2/#Draw), it isn't described here again.

The  `FlushResourceBarriers`  method is used on line 1022 to ensure that any  _non-pending_  resource barriers are flushed to the command list before executing the  `Draw`command.

On lines 1024-1027, the  `[DynamicDescriptorHeap::CommitStagedDescriptorsForDraw](https://www.3dgep.com/learning-directx12-3/#DynamicDescriptorHeapCommitStagedDescriptors)`method is use to ensure all of the resource descriptors are bound to the graphics pipeline.

The
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMxNTkyODkyM119
-->