```
cd ~/catkin_ws/src
git clone https://github.com/RainerKuemmerle/g2o.git
```
```
cd g2o
mkdir build
cd build
cmake ..
make
sudo make install
```
```
#include <tuple>
#include <type_traits>
#include <utility>

namespace g2o {

template <typename F, typename T, std::size_t... I>

void tuple_apply_i_(F&& f, T& t, int i, std::index_sequence<I...>) {
  (..., (I == i ? f(std::get<I>(t)) : void()));
}

template <typename F, typename T>
void tuple_apply_i(F&& f, T& t, int i) {
  tuple_apply_i_(
      f, t, i, std::make_index_sequence<std::tuple_size<std::decay_t<T>>>());
}

}  // namespace g2o
```
```
#include <tuple>
#include <type_traits>
#include <utility>

namespace g2o {

template <typename F, typename T, std::size_t... I>
void tuple_apply_i_(F&& f, T& t, int i, std::index_sequence<I...>) {
    // 使用循环代替折叠表达式
    // 这里我们使用一个 lambda 来进行条件判断
    ((I == static_cast<std::size_t>(i)) ? f(std::get<I>(t)) : void(), ...);
}

template <typename F, typename T>
void tuple_apply_i(F&& f, T& t, int i) {
    tuple_apply_i_(
        std::forward<F>(f), t, i, std::make_index_sequence<std::tuple_size<std::decay_t<T>>::value>());
}

}  // namespace g2o
```
```
// g2o - General Graph Optimization
// Copyright (C) 2011 R. Kuemmerle, G. Grisetti, W. Burgard
// All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
// * Redistributions of source code must retain the above copyright notice,
//   this list of conditions and the following disclaimer.
// * Redistributions in binary form must reproduce the above copyright
//   notice, this list of conditions and the following disclaimer in the
//   documentation and/or other materials provided with the distribution.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
// IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
// TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
// PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED
// TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
// PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
// LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
// NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
// SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

#ifndef G2O_MATRIX_STRUCTURE_H
#define G2O_MATRIX_STRUCTURE_H

#include <string_view>

#include "g2o_core_api.h"

namespace g2o {

/**
 * \brief representing the structure of a matrix in column compressed structure
 * (only the upper triangular part of the matrix)
 */
class G2O_CORE_API MatrixStructure {
 public:
  MatrixStructure();
  ~MatrixStructure();
  /**
   * allocate space for the Matrix Structure. You may call this on an already
   * allocated struct, it will then reallocate the memory + additional space
   * (double the required space).
   */
  void alloc(int n_, int nz);

  void free();

  /**
   * Write the matrix pattern to a file. File is also loadable by octave, e.g.,
   * then use spy(matrix)
   */
  bool write(std::string_view filename) const;

  int n;     ///< A is m-by-n.  n must be >= 0.
  int m;     ///< A is m-by-n.  m must be >= 0.
  int* Ap;   ///< column pointers for A, of size n+1
  int* Aii;  ///< row indices of A, of size nz = Ap [n]

  //! max number of non-zeros blocks
  int nzMax() const { return maxNz; }

 protected:
  int maxN;   ///< size of the allocated memory
  int maxNz;  ///< size of the allocated memory
};

}  // namespace g2o

#endif
```
