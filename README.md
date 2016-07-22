# Trainslation01
这个可以输入文本并发送到另一个View上，用户可以通过点击View上的单词来获得该单词的翻译。
以下这一段代码是在点击发送按钮后，系统根据我所输入的句子，以空格为标志对句子进行切割成一个个的字符串，再生成一个个的Label，
依据字体的大小对Label的宽度做宽度自适应。最后进行排版。之前在公司中，我为了其他的一些功能可以更方便切入，因此用的是瀑布流的
方式来进行布局，因为这里并不打算引入得太深就随便进行了一下布局就算了，如有兴趣课自行修改。

NSArray * array = [self.WriteView.text componentsSeparatedByString:@" "];
    int j = 0;
    for (int i = 0; i < array.count; i++)
    {
        UILabel * label = [[UILabel alloc]init];
        label.font = [UIFont boldSystemFontOfSize:14.0f];
        label.text = [NSString stringWithFormat:@"%@",array[i]];
        label.tag = i+1;
        CGSize size = [array[i] sizeWithFont:label.font constrainedToSize:CGSizeMake(MAXFLOAT, label.frame.size.height)];
        if (i == 0) {
            UILabel * LABEL = [[UILabel alloc]initWithFrame:CGRectMake(0, 0, 0, 0)];
            self.lastLabel = LABEL;
        }
        CGFloat X =self.lastLabel.frame.size.width + self.lastLabel.frame.origin.x;
     
        [label setFrame:CGRectMake( X + 5,30 * j, size.width, 30)];
        CGFloat Length = label.frame.origin.x + label.frame.size.width;
        if (Length > self.ReadView.frame.size.width) {
            [label setFrame:CGRectMake(0, 30 * (j+1), size.width, 30)];
            j++;
        }
        UITapGestureRecognizer *tap=[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(tap)];
        [label addGestureRecognizer:tap];
        [self.ReadView addSubview:label];
        self.lastLabel = label;
