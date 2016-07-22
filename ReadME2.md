#这一段代码读者可以上网自己去找，因为我之前做得那款Apps用的也是“有道词典”的API,读者需要先在“有道词典”的网站上面申请到
YOUDAO_Keyfrom，以及YOUDAO_Key的邀请码,网上有详细的教程。



 NSString * strURL = [NSString stringWithFormat:@"http://fanyi.youdao.com/openapi.do?keyfrom=%@&key=%@&type=data&doctype=json&version=1.1&q=%@",YOUDAO_Keyfrom,YOUDAO_Key,[string stringByAddingPercentEncodingWithAllowedCharacters:[NSCharacterSet URLQueryAllowedCharacterSet]]];
    NSError *err = nil;
    NSArray *strResult;
    if (strURL!=nil) {
        NSURL * url = [NSURL URLWithString:strURL];
        NSData *data = [NSData dataWithContentsOfURL:url];
        NSDictionary *dictionary = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingMutableLeaves error:&err];
        strResult = [dictionary objectForKey:@"translation"];
        
    }
    if (err) {
        return [NSString stringWithFormat:@"error = %@",[err description]];
    }
    else
    {
        return [NSString stringWithFormat:@"%@",strResult[0]];
    }
