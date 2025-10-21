# 一、dataset
1.正负样本、难易样本
2.数据标注
3.数据增强
# 二、start
1.选择网络结构
	选择一个相似任务，通用的模型
2.选择优化器
	选择一个广泛应用的优化器
3.选择batch size
	选择硬件可支持的最大batch size
4.初始化配置（简单、避免花里胡哨）
	(1) the model configuration (e.g. number of layers)
	(2) the optimizer hyperparameters (e.g. learning rate)	
	(3) the number of training steps
# 三、tune   
1. Choosing the goal for the next round of experiments
	- Try a potential improvement to the pipeline (e.g. a new regularizer, preprocessing choice, etc.).
	- Understand the impact of a particular model hyperparameter (e.g.  activation function)	
	- Greedily minimize validation error.	
2. Designing the next round of experiments
	- Identifying scientific, nuisance, and fixed hyperparameters
	- Creating a set of studies
	- Striking a balance between informative and affordable experiments		 
3. Extracting insight from experimental results
	- Identifying bad search space boundaries
	-   Not sampling enough points in the search space
	- Examining the training curves
	- Detecting whether a change is useful with isolation plots
	- Automate generically useful plots
4. Determining whether to adopt a training pipeline change or hyperparameter configuration