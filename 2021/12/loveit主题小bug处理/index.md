# LoveIt主题小bug处理


在「文章」也就是posts/下，这个日期，没有问题，如“01-02”  
而在文章的详情中，标题下方及「更新于」后的，日期都会混乱。  
我先试着调整archetype/default中{{.Date}}，无效。  
后试着调整config.toml中的「dateFormat」也无效。但是此时，注意到，配置中关于date的参数就三个，分别填写了"2006-01-02""01-02""01-02"，  
而themes/LoveIt/layouts/partials/single/footer.html中是有默认值处理即default "2006-01-02"。

<font color = "red">所以，我尝试，去除了config.toml中dateFormat的值，改为""。随后正常了</font>

