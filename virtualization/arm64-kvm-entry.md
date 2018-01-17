



* kvm_arch_hardware_init
	* __hyp_set_vectors(kvm_get_idmap_vector())
		* 初始化vbar_el2为__kvm_hyp_init
		* 这应该就是为了下面的函数准备
		* 只有一个entry是有效的，就是__do_hyp_init
		* 而且x0, x1, x2就是下面传入的参数，x2就是hyp vector
	* __cpu_init_hyp_mode(pgd_ptr, hyp_stack_ptr, vector_ptr);
		* 设置是__kvm_hyp_vector为异常向量
		* 可以研究其中的el1_sync向量
* el1_sync 注释已经标注为guest trapped into EL2
	* stp x0, x1, [sp, #-16]!
		* 把x0, x1存入栈
		* 然后利用x0, x1进行判断
	* __guest_exit
		* 执行guest状态保存
		* save_callee_saved_regs 保存guest callee寄存器
		* restore_callee_saved_regs 恢复host callee寄存器
		* ret 应该是返回host了
			* 而且是返回__guest_enter之后
		* 在arch/arm64/kvm/hyp/entry.S
			* 这个文件还是有__guest_enter
* __guest_enter
	* save_callee_saved_regs 保存host callee寄存器
	* 还保存了x1到栈中
		* 必须吗？其实马上就返回了
	* 加载guest状态
	* eret
		* 进入guest

