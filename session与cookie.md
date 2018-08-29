#转发与重定向
	1）重定向写法：response.sendRedirect()
	转发写法：request.getRequestdispatcher().forward()
	2）URL地址不同  重定向显示的资源的路径地址  转发显示的是请求servlet的地址
	3）请求不同   转发：客户端只发送一次请求 返回状态码为200，OK  request作用域丢失
				 重定向：客户端首先向服务器端发送一次请求，服务器端返回请求结果及第二次访问所
				 需要的信息，之后会进行二次访问  可以发生在不同服务器上  状态码为302 fond
	4）速度不同：转发在同一台服务器上发生，效率稍高    重定向两次请求，效率稍慢
	5）生活例子： 转发：小明去商店买西瓜，商店没有，商店买来卖给小明 
				 重定向：小明去商店买西瓜，商店没有，老板告诉小明去哪买，然后小明自己去买

#cookie
	概念：饼干   服务器端发送给客户端，并且在客户端保存的一份小数据。数据形式：key-value
	原因：http连接是无状态的连接，因此服务器端不知道这是客户端的第几次访问，以及之前访问了
		什么内容，因此为了更好的用户体验和用户交互，产生cookie
	应用场景：自动登录（记录用户账号、密码）  浏览记录
	获取cookie、添加cookie；  会话cookie  持久化cookie
	安全问题：cookie保存在客户端上，会有一定的安全隐患，且cookie的大小和数量存在一定的限制
	
	
	
#JSP与servlet
	1）本质相同  jsp实际上也是一个servlet，将其变异后会生成对应的servlet类以及编译的字节码，
		内含初始化init、service、destroy等函数
	2）作用不同  servlet用于动态逻辑处理 侧重于逻辑控制  jsp现用于动态页面展示 侧重于视图
	
	
#session
	概念：会话  session是基于cookie的一种会话机制，是存放于服务器端的数据。在同一个域名下的
		多次请求访问都属于同一个会话。
	使用：request.getSession   cookie中存储sessionID
	生命周期：创建：在servlet中调用request.getSession   销毁:session存储在服务器上，可以进行
		持久化。销毁的情况：1.关闭服务器   2.session会话时间过期
	应用场景：克服cookie存储数据大小的限制（添加购物车）
