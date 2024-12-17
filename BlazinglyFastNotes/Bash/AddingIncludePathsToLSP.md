* For `clangd` going into the environment variables and adding 
```bash
export CPATH="/path/to/include/"
```
* fixed the issues with my `clangd` lsp not picking up certain header files. You must add the parent directory to the path you are specifying. 
* i.e. if I am trying to do
```cpp
#include <absl/synchronization/mutex.h>
```
* I need to have everything up to `absl` on the path