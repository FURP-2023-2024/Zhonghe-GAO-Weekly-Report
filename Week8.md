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
