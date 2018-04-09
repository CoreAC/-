关于业务凭证的制作要点.

一. 细表的数据源绑定流程.
1.在FormView中上方的标签中加入细表的info类型
例如: 
[NotNullValidate(typeof(NRCrsInfo),typeof(NRCrsAInfo))]

其中 typeof(NRCrsAInfo) 就是加入细表的模型.

2.在formView的构造函数中将细表的数据源给细表的info类型.
例如: 
public CrsFormView()
        {
            InitializeComponent();
            this.bdsMainData.DataSource = typeof(NRCrsInfo);
            this.bdsLineData.DataSource = typeof(NRCrsAInfo);
        }
3.在成员属性中的重写方法里边,把数据源设置为细表的数据源.
例如:
 protected override Record Record
        {
            get { return bdsMainData.DataSource as NRCrsInfo; }
            set
            {
                bdsMainData.DataSource = value;
                bdsLineData.DataSource = (value as NRCrsInfo).LineList;
            }
        }
4.给细表的所在控件控制器绑定上数据源. 通过控件属性直接绑定.
