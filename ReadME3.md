#最后生成的翻译需要通过点击一个Label,这样就必须从父控件中取出全部的子控件，有一点要注意的是，通常来说父控件的第一个子控件会是他自己

-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event
{
    UITouch *touch = touches.anyObject;
    for (int i = 0; i < self.ReadView.subviews.count; i++)
    {
      UILabel *lable = (UILabel *)[self.ReadView viewWithTag:i+1];
      BOOL flag = [lable pointInside:[touch locationInView:lable] withEvent:nil];
      if (flag)
      {
        self.ReadView.subviews[i].backgroundColor = [UIColor blueColor];
          NSString *getStr = [self translateText:lable.text];
          NSLog(@"%@",getStr);
      }
    }
}
