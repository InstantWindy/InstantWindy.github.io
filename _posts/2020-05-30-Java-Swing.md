## Java-Swing

[TOC]



### Swing相关链接

- [阿发java](http://afanihao.cn/java/index.html;jsessionid=A907A7D57BA5BE05334FE59292790FD5)

### Swing与AWT

- ![image-20200531220327477](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200531220327477.png)

### 中间面板Jpanel

- 面板组件，非顶层容器。一个界面只可以有一个JFrame窗体组件，但是可以有多个JPanel面板组件，而JPanel上也可以使用FlowLayout，BorderLayout，GridLayout等各种布局管理器，这样可以组合使用，达到较为复杂的布局效果。

- ![image-20200602204616405](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602204616405.png)

- ![image-20200602204746916](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602204746916.png)

  ```
  import javax.swing.*;
  
  import java.awt.*;  //引入AWT包，因为要使用到颜色类
  
  class PanelDemo {
  
           public static void main(String[] args)throws Exception
  
           {   JFrame f=new JFrame("第一个Java窗口");                   
  
  f.setSize(300,200);         
  
                f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
  
          f.setVisible(true);         
  
                  f.setResizable(false);
  
                  f.setLocationRelativeTo(null) ;
  
                     f.setLayout(null);  //设置窗体布局为空布局
  
                  JPanel p=new JPanel();             //实例化一个面板
  
                     //设置面板背景色为蓝色，如果不引入AWT包，程序将出错，可以试试看
  
                  p.setBackground(Color.BLUE);       
  
                  p.setSize(100,100);          //设置面板对象大小
  
                  f.getContentPane().add(p);     //将面板添加到窗体中
  
                     //如果使用下面添加面板的方法，面板将布满整个窗口，可以试试看
  
                     //f. setContentPane(p);
  
            }
  
  }
  
  ```

  

### 标签JLabel

- ![image-20200531224125396](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200531224125396.png)

### 文本框 JTextField

- ![image-20200531225826612](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200531225826612.png)

``````
package com.Swing;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MyFrameDemo extends JFrame {
    JLabel label =new JLabel("姓名");
    JTextField textField = new JTextField(16);
    JButton button = new JButton("确定");

    public MyFrameDemo(String title) {
        super(title);
        // 内容面板（contentPane）
        Container contentPane = getContentPane();
        contentPane.setLayout(new FlowLayout());
        contentPane.add(label);
        contentPane.add(textField);
        contentPane.add(button);
        // 按钮点击处理
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                onButtonOk();
            }
        });
    }
    private void onButtonOk(){
        // 取得文本框中的输入值
        String str = textField.getText();
        // 弹出一个对话框
        JOptionPane.showMessageDialog(this,"输入了："+str);
    }

}


``````

### 复选框JCheckBox

- ![image-20200601215824426](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200601215824426.png)

```
public class MyFrame extends JFrame
{
    JCheckBox cbx = new JCheckBox("我想订阅邮件通知");
    JTextField email = new JTextField(16);
    public MyFrame(String title)
    {
        super(title);
		// 内容面板 (ContentPane)
        Container contentPane = getContentPane();
        contentPane.setLayout(new FlowLayout());
		// 添加控件
        contentPane.add(cbx);
        contentPane.add(email);
        cbx.setSelected(true); // 默认选中
        email.setToolTipText("输入邮箱地址");

        cbx.addActionListener( new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e)
            {
				// 如果未选中，则禁用文本框
                if(cbx.isSelected())
                    email.setEnabled(true);
                else
                    email.setEnabled(false);
            }
        });
    }
}

```

### 下拉列表JComboBox

```
JComboBox<String> colorList = new JComboBox<>();
colorList.addItem("红色");
colorList.addItem("蓝色");
colorList.addItem("绿色");
// 使用索引，可以访问下拉列表中的每一项。
T value = colorList.getItemAt( index) ; // 获取第几项
int count = colorList.getItemCount(); // 一共多少项
-  getSelectedIndex() ，获取当前选中项的索引
-  setSelectedIndex(index) ，设置当前选中项
-  remove(index)，删除一项
-  T value = getSelectedItem()，获取当前项的值
-  setSelectedItem(value) ，设置当前选中值，内部会按值用 equals()比较
-  remove(value)，删除一项，内部会按值用 equals()比较
```

```
package com.Swing;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MyFrameOne extends JFrame {
//    JComboBox<String> colorList = new JComboBox<>();
    JComboBox<ListOption> colorList = new JComboBox<>();
    JLabel simpleText = new JLabel("This is a simple text");
    public MyFrameOne(String title){
        super(title);
        // 内容面板 (ContentPane)
        Container contentPane = getContentPane();
        contentPane.setLayout(new FlowLayout());
        // 添加控件
        contentPane.add(colorList);
        contentPane.add(simpleText);
        colorList.addItem( new ListOption("红色", Color.RED));
        colorList.addItem( new ListOption("绿色", Color.GREEN));
        colorList.addItem( new ListOption("蓝色", Color.BLUE));

//        colorList.addItem("Green");
//        colorList.addItem("Red");
//        colorList.addItem("Blue");
        updateTextColor();

        colorList.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                updateTextColor();
            }
        });

    }
    // 更新Jlabel颜色显示
    private void updateTextColor(){
        // 获取选中项的值
        ListOption item = (ListOption)colorList.getSelectedItem();
//        String item = (String) jComboBox.getSelectedItem();
//        // 根据选择颜色，设置
//        Color color = null;
//        if (item.equals("Red"))
//            color = Color.RED;
//        else if(item.equals("Blue"))
//            color = Color.BLUE;
//        else if (item.equals("Green"))
//             color = Color.GREEN;
        simpleText.setForeground(item.color);
    }
    private static class ListOption // static class，静态内部类
    {
        public String text;
        public Color color;
        public ListOption(String text, Color color)
        {
            this.text = text;
            this.color = color;
        }
        @Override
        public String toString() // 重定 toString()用于列表项的显示
        {
            return "[" + this.text + "]" ;
        }
    }
}

```

### 布局管理器

#### 流布局FlowLayout

- <img src="C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200601223030102.png" alt="image-20200601223030102" style="zoom:60%;" />

- <img src="C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200601223047398.png" alt="image-20200601223047398" style="zoom:60%;" />

  ```
  Container contentPane = getContentPane();
  LayoutManager layout = new FlowLayout(FlowLayout.LEFT);
  contentPane.setLayout(layout);
  
  ```

#### 边界布局BorderLayout

- 边界布局管理器把容器的的布局分为五个位置：CENTER、EAST、WEST、NORTH、SOUTH。依次相应为：上北（NORTH）、下南（SOUTH）、左西（WEST）、右东（EAST），中（CENTER）。

  -  能够把组件放在这五个位置的随意一个，假设未指定位置，则缺省的位置是CENTER。
  -  南、北位置控件各占领一行，控件宽度将自己主动布满整行。东、西和中间位置占领一行;若东、西、南、北位置无控件，则中间控件将自己主动布满整个屏幕。若东、西、南、北位置中不管哪个位置没有控件，则中间位置控件将自己主动占领没有控件的位置。

- ![image-20200602203035191](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602203035191.png)

  ```
  contentPane.setLayout(new BorderLayout());
  JLabel a1 = new ColorfulLabel("1", Color.YELLOW);
  JLabel a2 = new ColorfulLabel("2", Color.GREEN);
  JLabel a3 = new ColorfulLabel("3", Color.LIGHT_GRAY);
  JLabel a4 = new ColorfulLabel("4", Color.CYAN);
  JLabel a5 = new ColorfulLabel("5", Color.WHITE);
  contentPane.add(a1, BorderLayout.PAGE_START); // 上
  contentPane.add(a2, BorderLayout.PAGE_END); // 下
  contentPane.add(a3, BorderLayout.LINE_START); // 左
  contentPane.add(a4, BorderLayout.LINE_END); // 右
  contentPane.add(a5, BorderLayout.CENTER); // 中
  ```

  

#### 卡片布局CardLayout

- <img src="C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602210617246.png" alt="image-20200602210617246" style="zoom:40%;" />
- <img src="C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602210640971.png" alt="image-20200602210640971" style="zoom:50%;" />

```
package com.Swing;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.jar.JarEntry;

public class MyFrame2 extends JFrame {
    JComboBox<String > options = new JComboBox<>();
    JPanel card = new JPanel();

    public MyFrame2(String title){
        super(title);

        Container container = getContentPane();
        container.setLayout(new BorderLayout());

        // 创建一个下拉列表选择
        options.addItem("第一个面板");
        options.addItem("第二个面板");
        container.add(options,BorderLayout.PAGE_START);
        container.add(card,BorderLayout.CENTER);

        // 创建第一个面板
        JPanel p1 = new JPanel();
        p1.add(new JButton("红"));
        p1.add(new JButton("绿"));
        p1.add(new JButton("蓝"));

        // 创建第二个面板
        JPanel p2 = new JPanel();
        p2.add(new JLabel("输入"));
        p2.add(new JTextField(16));

        card.setLayout(new CardLayout());
        card.add(p1,"buttons");
        card.add(p2,"text");

        options.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                itemChanged();
            }
        });
    }
    private void itemChanged(){
       CardLayout cardLayout= (CardLayout) card.getLayout();
       int idx = options.getSelectedIndex();
       if(idx==0){
           cardLayout.show(card,"buttons");
       }
       else if(idx==1)
           cardLayout.show(card,"text");
    }
}

```



### 自定义布局

#### 窗口坐标

- 当在一个容器（Container）里添加多个子控件（Component）时，容器要负责
  子控件的布局。所谓布局，就是决定把每个控件放在什么位置、宽高是多大。在 Swing 里，使用 Rectangle 类来描述一个子控件的位置和大小。例如，`Rectangle rect = new Rectangle(30,30,200,100);`则此矩形描述的是左上角坐标为(30,30)，宽度 200 像素，高度 100 像素.

  ```
  public MyFrame(String title)
  {
  super(title);
  Container root = this.getContentPane();
  root.setLayout(null); // 取消其布局器
  // 增加 2 个控件
  JLabel a1 = new ColorfulLabel("1", Color.yellow);
  JLabel a2 = new ColorfulLabel("2", Color.blue);
  root.add(a1);
  root.add(a2);
  // 用来设置控件显示位置
  a1.setBounds(new Rectangle(0,0, 200,200));
  a2.setBounds(new Rectangle(100,100, 200,100));
  }
  
  private static class ColorfulLabel extends JLabel
  {
      public ColorfulLabel(String text, Color bgColor)
      {
          super(text);
          setOpaque(true);
          setBackground(bgColor);
          setPreferredSize(new Dimension(60,30));
          setHorizontalAlignment(SwingConstants.CENTER);
      }
  }
  ```

  

#### 创建布局器

- 自定义布局器时，需要创建一个类，实现 LayoutManager 接口。例如，在
  MyFrame 里添加一个内部类 SimpleLayout，示例如下

```
JLabel a1 = new JLabel("Hello");
JLabel a2= new JLabel("样例文本");
private class SimpleLayout implements LayoutManager
{
    public void addLayoutComponent(String name, Component comp){}
    public void removeLayoutComponent(Component comp){}
    public Dimension preferredLayoutSize(Container parent){}
    public Dimension preferredLayoutSize(Container parent){}
    // 当窗口大小改变（或其他情况时），内部会自动调用 SimpleLayout.layoutContainer() 来重新布局
    public void layoutContainer(Container parent) {

        int w = parent.getWidth(); // 父窗口的宽度 width
        int h = parent.getHeight(); // 父窗口的高度 height
        System.out.println("父容器: " + w + ", " + h);
        // a1 显示在中间, 以 Preferred Size 作为大小
        if (a1.isVisible()) {
            // 得取该控件所需的显示尺寸
            Dimension size = a1.getPreferredSize();
            //System.out.println(size);
            int x = (w - size.width) / 2;
            int y = (h - size.height) / 2;
             // 在设置子控件位置时，其坐标是相对于父窗口的
             // (0,0) 就是父窗口的左上角
            a1.setBounds(x, y, size.width, size.height);
        }
        // a2 显示在右上角
        if (a2.isVisible()) {
            Dimension size = a2.getPreferredSize();
            //System.out.println(size);
            int x = (w - size.width);
            int y = 0;
            a2.setBounds(x, y, size.width, size.height);
        }
    }
    }
}

// 运行
Container root = this.getContentPane();
root.setLayout(new SimpleLayout())
```

#### 线性布局

- 线性布局，指的是在水平方向上依次布局，或者上竖直方向上依次布局。这
  是在实际项目中最常见的布局方式。这里提供两个方便易用的布局器，分别用于
  水平和竖直方式上的布局。

  ```
  package my;
  
  import java.awt.Color;
  import java.awt.Component;
  import java.awt.Container;
  import java.awt.Dimension;
  import java.awt.Font;
  import java.awt.LayoutManager;
  
  import javax.swing.JFrame;
  import javax.swing.JLabel;
  import javax.swing.JPanel;
  import javax.swing.SwingConstants;
  
  import af.swing.layout.AfXLayout;
  
  public class MyFrame extends JFrame
  {
  	JLabel a1 = new ColorfulLabel("Hello,World", Color.yellow);
  	JLabel a2 = new ColorfulLabel("样例文本", Color.blue);
  	JLabel a3 = new ColorfulLabel("Good Boy", Color.CYAN);
  	JLabel a4 = new ColorfulLabel("占满剩余", Color.red);
  	
  	public MyFrame(String title)
  	{
  		super(title);
  		
  		// 根容器
  		JPanel root = new JPanel();
  		this.setContentPane(root);
  		
  		// 设置为横向布局 
  		// 注: AfXLayout 与 AfRowLayout等效
  		root.setLayout(new AfXLayout(8)); // 子控件之间的间距为8像素
  		
  		root.add(a1, "100px"); // 固定占100像素
  		root.add(a2, "30%");  // 固定占30%
  		root.add(a3, "auto"); // 按 Preferred Size 设置
  		root.add(a4, "1w");   // 按权重设置，权重为1 weight
  	}
  	
  	
  	// ColorfulLabel: 参考4.5节的讲解
  	private static class ColorfulLabel extends JLabel
  	{
  		public ColorfulLabel(String text, Color bgColor)
  		{
  			super(text);
  			
  			setOpaque(true);
  			setBackground(bgColor);
  			//setPreferredSize(new Dimension(60,30));
  			setHorizontalAlignment(SwingConstants.CENTER);
  			setFont(new Font("宋体", Font.PLAIN, 16));
  		}
  	}
  	
  	
  }
  
  ```

  

##### 水平布局

- ![image-20200602220540004](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602220540004.png)

  ```
  package af.swing.layout;
  
  import java.awt.Component;
  import java.awt.Container;
  import java.awt.Dimension;
  import java.awt.Insets;
  import java.awt.LayoutManager;
  import java.awt.LayoutManager2;
  import java.awt.Rectangle;
  import java.util.ArrayList;
  import java.util.Iterator;
  import java.util.List;
  
  import javax.swing.JPanel;
  
  /* 横向布局器，和 AfXLayout 等效 
   * 
   */
  public class AfRowLayout implements LayoutManager2
  {
  	private List<Item> items = new ArrayList<>();
  	private int gap = 2;
  	private boolean usePerferredSize = false; // 竖立方向是否占满
  	
  	public AfRowLayout()
  	{		
  	}
  	public AfRowLayout(int gap)
  	{		
  		this.gap = gap; // 控件之间的间距
  	}
  	public AfRowLayout(int gap, boolean usePerferredSize)
  	{	
  		this.gap = gap;
  		this.usePerferredSize = usePerferredSize;
  	}
  		
  	@Override
  	public void addLayoutComponent(String name, Component comp)
  	{
  		Item item = new Item();
  		item.comp = comp;
  		item.constraints = "auto";
  		items.add(item);
  	}
  
  	@Override
  	public void removeLayoutComponent(Component comp)
  	{
  		Iterator<Item> iter = items.iterator();
  		while(iter.hasNext())
  		{
  			Item item = iter.next();
  			if(item.comp == comp)
  			{
  				iter.remove();
  			}
  		}
  	}
  
  	@Override
  	public void addLayoutComponent(Component comp, Object constraints)
  	{
  		Item item = new Item();
  		item.comp = comp;
  		item.constraints = (String) constraints;
  		items.add(item);
  	}
  	
  	@Override
  	public Dimension preferredLayoutSize(Container parent)
  	{
  		return new Dimension(30,30);
  	}
  
  	@Override
  	public Dimension minimumLayoutSize(Container parent)
  	{
  		return new Dimension(30,30);
  	}
  
  	@Override
  	public Dimension maximumLayoutSize(Container target)
  	{
  		return new Dimension(30,30);
  	}
  
  	
  	@Override
  	public void layoutContainer(Container parent)
  	{
  		// 得到内矩形
  		Rectangle rect = new Rectangle(parent.getWidth(), parent.getHeight());
  		//Rectangle rect = parent.getBounds();
  		Insets insets = parent.getInsets();
  		rect.x += insets.left;
  		rect.y += insets.top;
  		rect.width -= (insets.left + insets.right);
  		rect.height -= (insets.top + insets.bottom);
  		
  		// 第一轮：过滤到无效的 Item ( 有些控件是隐藏的 )
  		List<Item> validItems = new ArrayList<>();
  		for(Item it: items )
  		{
  			if(it.comp.isVisible())
  				validItems.add(it);
  		}
  		
  		// 第二轮处理：百分比，像素，auto的，直接计算出结果; 权重的，在第三轮计算
  		int totalGapSize = gap * (validItems.size() - 1);// 间距大小
  		int validSize = rect.width - totalGapSize;
  		int totalSize = 0;
  		int totalWeight = 0;
  		for(Item it : validItems)
  		{
  			Dimension preferred = it.comp.getPreferredSize();
  			it.width = preferred.width;
  			it.height = usePerferredSize ? preferred.height : rect.height;
  			it.weight = 0;
  			
  			// 计算宽度
  			String cstr = it.constraints;
  			if( cstr == null || cstr.length() == 0)
  			{
  				//System.out.println("(AfRowLayout) Warn: Must define constraints when added to container!");
  			}
  			else if( cstr.equals("auto"))
  			{
  			}
  			else if(cstr.endsWith("%")) // 按百分比
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-1));
  				it.width = validSize * num / 100;
  			}
  			else if(cstr.endsWith("w")) // 按权重
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-1));
  				it.width = 0;
  				it.weight = num;
  			}
  			else if(cstr.endsWith("px")) // 按权重
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-2));
  				it.width = num;
  			}
  			else // 按像素
  			{
  				int num = Integer.valueOf(cstr);
  				it.width = num;
  			}
  			
  			totalSize += it.width;
  			totalWeight += it.weight;
  			
  			//System.out.println("计算值：width=" + it.width + ",weight=" + it.weight);
  		}
  		
  		// 第三轮: 剩余空间按权重分配
  		if( totalWeight > 0)
  		{
  			int remainSize = validSize - totalSize;
  			double unit = (double) remainSize / totalWeight;
  			for(Item it : validItems)
  			{
  				if(it.weight > 0)
  				{
  					it.width = (int)( unit * it.weight );
  				}
  			}			
  		}
  
  		//System.out.println("总宽度: " + rect.width);
  		
  		// 第四轮: 按宽度和高度布局
  		int x = 0;
  		for(Item it : validItems)
  		{
  			int y = (rect.height - it.height)/2;
  			if(x + it.width > rect.width)
  				it.width = rect.width - x;
  			if(it.width <= 0) break;
  			
  			it.comp.setBounds(rect.x + x, rect.y + y, it.width, it.height);
  			
  			//System.out.println("宽度: " + it.width);
  			x += it.width;
  			x += gap; // 间距
  		}
  	}
  
  	@Override
  	public float getLayoutAlignmentX(Container target)
  	{
  		return 0;
  	}
  
  	@Override
  	public float getLayoutAlignmentY(Container target)
  	{
  		return 0;
  	}
  
  	@Override
  	public void invalidateLayout(Container target)
  	{
  		
  	}
  
  	///////////////////////
  	private static class Item
  	{
  		Component comp;
  		String constraints = "auto";
  		int width = 0;
  		int height = 0;
  		int weight = 0;  // 权重
  	}
  	
  
  }
  
  
  package af.swing.layout;
  
  /* 横向布局器，和 AfRowLayout 等效 
   * 
   */
  public class AfXLayout extends AfRowLayout
  {
  	public AfXLayout()
  	{		
  	}
  	public AfXLayout(int gap)
  	{		
  		super(gap);
  	}
  	public AfXLayout(int gap, boolean usePerferredSize)
  	{	
  		super(gap, usePerferredSize);
  	}
  }
  ```

##### 垂直布局

- ![image-20200602220830919](C:\Users\Insta\AppData\Roaming\Typora\typora-user-images\image-20200602220830919.png)

  ````
  package af.swing.layout;
  
  import java.awt.Component;
  import java.awt.Container;
  import java.awt.Dimension;
  import java.awt.Insets;
  import java.awt.LayoutManager;
  import java.awt.LayoutManager2;
  import java.awt.Rectangle;
  import java.util.ArrayList;
  import java.util.Iterator;
  import java.util.List;
  
  import javax.swing.JPanel;
  
  /* 纵向布局器，和 AfYLayout 等效 
   * 
   */
  public class AfColumnLayout implements LayoutManager2
  {
  	private List<Item> items = new ArrayList<>();
  	private int gap = 2;
  	private boolean usePerferredSize = false; // 竖立方向是否占满
  	
  	public AfColumnLayout()
  	{		
  	}
  	public AfColumnLayout(int gap)
  	{		
  		this.gap = gap; // 控件之间的间距
  	}
  	public AfColumnLayout(int gap, boolean usePerferredSize)
  	{	
  		this.gap = gap;
  		this.usePerferredSize = usePerferredSize;
  	}
  		
  	@Override
  	public void addLayoutComponent(String name, Component comp)
  	{
  		Item item = new Item();
  		item.comp = comp;
  		item.constraints = "auto";
  		items.add(item);
  	}
  
  	@Override
  	public void removeLayoutComponent(Component comp)
  	{
  		Iterator<Item> iter = items.iterator();
  		while(iter.hasNext())
  		{
  			Item item = iter.next();
  			if(item.comp == comp)
  			{
  				iter.remove();
  			}
  		}
  	}
  
  	@Override
  	public void addLayoutComponent(Component comp, Object constraints)
  	{
  		Item item = new Item();
  		item.comp = comp;
  		item.constraints = (String) constraints;
  		items.add(item);
  	}
  	
  	@Override
  	public Dimension preferredLayoutSize(Container parent)
  	{
  		return new Dimension(30,30);
  	}
  
  	@Override
  	public Dimension minimumLayoutSize(Container parent)
  	{
  		return new Dimension(30,30);
  	}
  
  	@Override
  	public Dimension maximumLayoutSize(Container target)
  	{
  		return new Dimension(30,30);
  	}
  
  	
  	@Override
  	public void layoutContainer(Container parent)
  	{
  		// 得到内矩形
  		Rectangle rect = new Rectangle(parent.getWidth(), parent.getHeight());
  		//Rectangle rect = parent.getBounds();
  		Insets insets = parent.getInsets();
  		rect.x += insets.left;
  		rect.y += insets.top;
  		rect.width -= (insets.left + insets.right);
  		rect.height -= (insets.top + insets.bottom);
  		
  		// 第一轮：过滤到无效的 Item ( 有些控件是隐藏的 )
  		List<Item> validItems = new ArrayList<>();
  		for(Item it: items )
  		{
  			if(it.comp.isVisible())
  				validItems.add(it);
  		}
  		
  		// 第二轮处理：百分比，像素，auto的，直接计算出结果; 权重的，在第三轮计算
  		int totalGapSize = gap * (validItems.size() - 1);// 间距大小
  		int validSize = rect.height - totalGapSize;
  		int totalSize = 0;
  		int totalWeight = 0;
  		for(Item it : validItems)
  		{
  			Dimension preferred = it.comp.getPreferredSize();
  			it.width = usePerferredSize ? preferred.width : rect.width;
  			it.height = preferred.height;
  			it.weight = 0;
  			
  			// 计算宽度
  			String cstr = it.constraints;
  			if( cstr == null || cstr.length() == 0)
  			{
  				//System.out.println("(AfColumnLayout) Warn: Must define constraints when added to container!");
  			}
  			else if( cstr.equals("auto"))
  			{
  			}
  			else if(cstr.endsWith("%")) // 按百分比
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-1));
  				it.height = validSize * num / 100;
  			}
  			else if(cstr.endsWith("w")) // 按权重
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-1));
  				it.height = 0;
  				it.weight = num;
  			}
  			else if(cstr.endsWith("px")) // 按权重
  			{
  				int num = Integer.valueOf(cstr.substring(0,cstr.length()-2));
  				it.height = num;
  			}
  			else // 按像素
  			{
  				int num = Integer.valueOf(cstr);
  				it.height = num;
  			}
  			
  			totalSize += it.height;
  			totalWeight += it.weight;
  			
  			//System.out.println("计算值：width=" + it.width + ",weight=" + it.weight);
  		}
  		
  		// 第三轮: 剩余空间按权重分配
  		if( totalWeight > 0)
  		{
  			int remainSize = validSize - totalSize;
  			double unit = (double) remainSize / totalWeight;
  			for(Item it : validItems)
  			{
  				if(it.weight > 0)
  				{
  					it.height = (int)( unit * it.weight );
  				}
  			}			
  		}
  
  		//System.out.println("总宽度: " + rect.width);
  		
  		// 第四轮: 按宽度和高度布局
  		int y = 0;
  		for(Item it : validItems)
  		{
  			int x = 0; // 水平靠左			
  			if(y + it.height > rect.height)
  				it.height = rect.height - y;
  			if(it.height <= 0) break;
  			
  			it.comp.setBounds(rect.x + x, rect.y + y, it.width, it.height);
  			
  			//System.out.println("宽度: " + it.width);
  			y += it.height;
  			y += gap; // 间距
  		}
  	}
  
  	@Override
  	public float getLayoutAlignmentX(Container target)
  	{
  		return 0;
  	}
  
  	@Override
  	public float getLayoutAlignmentY(Container target)
  	{
  		return 0;
  	}
  
  	@Override
  	public void invalidateLayout(Container target)
  	{
  		
  	}
  
  	///////////////////////
  	private static class Item
  	{
  		Component comp;
  		String constraints = "auto";
  		int width = 0;
  		int height = 0;
  		int weight = 0;  // 权重
  	}
  	
  
  }
  
  package af.swing.layout;
  
  /* 纵向布局器，和  AfColumnLayout 等效 
   * 
   */
  public class AfYLayout extends AfColumnLayout
  {
  	public AfYLayout()
  	{		
  	}
  	public AfYLayout(int gap)
  	{		
  		super(gap);
  	}
  	public AfYLayout(int gap, boolean usePerferredSize)
  	{	
  		super(gap, usePerferredSize);
  	}
  }
  
  ````

  

#### 综合布局

```
package my;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;

import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.SwingConstants;

import af.swing.layout.AfXLayout;
import af.swing.layout.AfYLayout;

public class MyFrame extends JFrame
{
	ColorfulLabel a1 = new ColorfulLabel("。。。", Color.YELLOW);
	ColorfulLabel a2 = new ColorfulLabel(">>>", Color.GREEN);
	JButton sendButton = new JButton("发送");
	
	public MyFrame(String title)
	{
		super(title);
		
		// 根容器
		JPanel root = new JPanel();
		this.setContentPane(root);
		
		// 总体上使用 BorderLayout
		root.setLayout(new BorderLayout());
		
		// 中间加一个控件
		root.add(a1, BorderLayout.CENTER); 
		
		// 上面是一个组合
		if( true )
		{
			// JPanel面板，其实就是一个容器
			JPanel p = new JPanel();
			p.setLayout(new AfXLayout(4));
			
			p.add(a2,"1w"); // 权重为1，水平方向占满剩余空间
			p.add(sendButton, "80px"); // 水平方向固定80像素宽度
			
			root.add(p,  BorderLayout.PAGE_START);
		}
	}

	// ColorfulLabel: 参考4.5节的讲解
	private static class ColorfulLabel extends JLabel
	{
		public ColorfulLabel(String text, Color bgColor)
		{
			super(text);
			
			setOpaque(true);
			setBackground(bgColor);
			//setPreferredSize(new Dimension(60,30));
			setHorizontalAlignment(SwingConstants.CENTER);
			setFont(new Font("宋体", Font.PLAIN, 16));
		}
	}	
}
```

