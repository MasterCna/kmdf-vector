# kmdf-vector
Pure C vector implementation optimized for Kernel-mode driver usage


Easy-to-use
```C
#include "vector.h"

  // Creates an empty vector with the default reserved size
  // and without custom deleter. Vector will contain 'int'
  vc_vector* v = vc_vector_create(0, sizeof(int), NULL);
  if (!v) {
    return 1;
  }

  const int count = 10;
  for (int i = 0; i < count; ++i) {
    // The function takes a pointer to the elements,
    // but the vector will make a copy of the element
    vc_vector_push_back(v, &i);
  }

  // Print each vector element
  for (void* i = vc_vector_begin(v);
             i != vc_vector_end(v);
             i = vc_vector_next(v, i)) {
    KdPrint(("%u; ", *(int*)i));
  }

  vc_vector_release(v);
```

## Main Implementation
From: https://github.com/skogorev/vc_vector
