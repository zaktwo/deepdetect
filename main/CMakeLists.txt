include_directories(${Boost_INCLUDE_DIRS})
link_directories(${CAFFE_LIB_DIR})
if (CUDA_FOUND)
  set(CUDA_LIB_DEPS -lcudart -lcublas -lcurand)# -lcudnn) #TODO: cudnn
else()
  add_definitions(-DCPU_ONLY)
endif()
set(CAFFE_LIB_DEPS -lleveldb -lsnappy -llmdb -lhdf5_hl -lhdf5 -lopenblas -lcaffe -lprotobuf)

add_executable (dede dede.cc)
target_link_libraries (dede ddetect glog gflags opencv_core opencv_highgui opencv_imgproc cppnetlib-uri curlpp curl crypto ssl ${Boost_LIBRARIES} ${CAFFE_LIB_DEPS})