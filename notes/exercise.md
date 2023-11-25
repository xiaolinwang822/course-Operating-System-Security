
1. 因为AVC中存储的访问决策是基于先前的策略生成的,当新策略加载到内核时,这些决策不再有效,必须刷新。
2. (1) AVC存在于内核空间,而用户空间对象管理器运行在用户空间。用户空间进程无法直接访问内核空间的AVC。  
(2)内核安全服务器可以根据当前最新的安全策略,计算每个访问请求的访问控制决定,并更新AVC。而用户空间对象管理器无法做到这一点,它无法保证AVC同步更新到最新的策略,可能导致错误或不安全决定。  
3. type_transition user_t games_exec_t : process games_t;  
    allow user_t games_exec_t : file execute;   
    allow user_t games_t:process transition;  
    allow  games_t games_exec_t : file entrypoint;  
4. role_transition sysadm_r initrc_exec_t : system_r;   
    allow sysadm_r system_r; 
5. validatetrans {feile lnk_file} 
( ( t3 == relabel_any) or   
( t2 != shadow_t) or
( t1 == user_tmp_t) );  
6. mlsconstrain file { write create setattr relabelfrom append  unlink link rename mounton }
(t1 == special_type)or((l1 dom l2) and (l2 dom l1));
