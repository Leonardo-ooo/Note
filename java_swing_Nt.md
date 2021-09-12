//java swing 学习笔记

~~~java
//JPanel默认布局为FlowLayout

setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);		//关闭所有窗口后退出程序
setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);	//只关闭本窗口，关闭后无窗口则退出程序
exit(),dispose() 	//事件响应用前者关闭所有窗口退出程序，后者仅关闭指定窗口

//在设置了Layout布局管理器时
setPreferredSize(new Dimension(int width,int height));		//设置组件显示大小
setMinimumSize(int width, int height); setMaximumSize(int width,int height);	//设置窗口最大，最小大小

FlowLayout(int align);	//设置组件对齐方式，默认左对齐

FlowLayout(int align, int hgap, int vgap); 	//设置组件上下，左右间距

BoderLayout(组件, BorderLayout.PAGE_START/PAGE_END/LINE_START/LINE_END/CENTER);	
//设置组件位置上，下，左，右，中

CardLayout

JCheckBox //复选框
setSelect()  //选中状态设置
isSelected() //判断是否选中

JComboBox	//下拉列表
addItem(String item_name); 		//增加选项
getSelectedIndex();		//获取选择选项序号（0开始）
getSelectedItem();		//获取选项，可以强制转换成String
~~~

