

## 共享内存

共享内存允许两个不相关的进程访问同一个逻辑内存。共享内存在同一个物理内存中，进程将同一段共享内存连接到自己的地址空间，某个进程对共享内存写入
数据，改动会立即影响到同一段共享内存的其他进程。 注意共享内存**未提供同步机制**。


* 创建共享内存
	* key: 函数成功返回与key值相关的共享内存标识符，失败返回-1；
	* size: 需要使用的共享内存容量
	* shmflg: 权限标志；比如0644允许一个进程创建的共享内存被内存创建者所拥有的进程进行读写数据，而其他进程只能读取共享内存；

```c++
int shmget(key_t key, size_t size, int shmflg);
```

* 启动共享内存的访问

```c++
void *shmat(int shm_id, const void *shm_addr, int shmflg);  
```

* 分离共享内存

用于将共享内存从当前进程分离，注意并不是删除共享内存。 `shmaddr`是`shmat`返回的地址指针，调用成功返回0，失败返回-1。

```c++
int shmdt(const void *shmaddr);  
```

* 控制共享内存
	* shm_id: shmget函数返回的共享内存标识
	* command: 要采取的操作(IPC_START, IPC_SET, IPC_RMID)
	* buf: 结构体指针，指向共享内存的访问模式和访问权限的结构


```c++
int shmctl(int shm_id, int command, struct shmid_ds *buf);    

struct shmid_ds  
{  
    uid_t shm_perm.uid;  
    uid_t shm_perm.gid;  
    mode_t shm_perm.mode;  
}; 
```