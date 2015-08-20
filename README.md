# codesnippet
iOS 代码片段

图片下载（来源：http://cocoanuts.mobi/2014/04/27/fastscroll/）

    - (void)downloadImageWithURL:(NSURL *)url completionBlock:(void (^)(BOOL succeeded, UIImage *image))completionBlock
    {
        NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
    [NSURLConnection sendAsynchronousRequest:request
                                       queue:[NSOperationQueue mainQueue]
                           completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {
                               if ( !error )
                               {
                                   UIImage *image = [[UIImage alloc] initWithData:data];
                                   completionBlock(YES,image);
                               } else{
                                   completionBlock(NO,nil);
                               }
                           }];
    }


宏定义Default

    #define DF_Defatlut [NSUserDefaults standardUserDefaults]
    //取Default值
    #define DF_DefaultsObjectForKey(key) [[NSUserDefaults standardUserDefaults] valueForKey:key]
    //存Default值 
    #define DF_DefaultsSetValueForKey(value,key) [[NSUserDefaults standardUserDefaults] setValue:value forKey:key]
    #define DF_DefaultRemoveValueForKey(key) [[NSUserDefaults standardUserDefaults] removeObjectForKey:key]
    #define DF_DefaultSynchronize [[NSUserDefaults standardUserDefaults] synchronize]


获取app的info.plist详细信息

    版本号：Bundle version
    NSString *version = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleVersion"];

    应用标识：Bundle identifier
    NSString *bundleId = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleIdentifier"];

    应用名称：Bundle display name
    NSString *appName = [[NSBundle mainBundle] objectForInfoDictionaryKey:@"CFBundleDisplayName"];

    Bundle name
    NSString *appName = [[NSBundle mainBundle] objectForInfoDictionaryKey:@"CFBundleName"];

直接取某个数据库宏定义

    #define kPath_FMDB [NSHomeDirectory() stringByAppendingPathComponent:@"Documents/xxx.sqlite"]

邮箱和手机号验证

    + (BOOL)isValidEmail:(NSString *)email {
        NSString *emailRegex = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";
    NSPredicate *emailTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegex];
    return [emailTest evaluateWithObject:email];
    }
    + (BOOL)isValidMobile:(NSString *)mobile {
    NSString *phoneRegex = @"^([0|86|17951]?(13[0-9])|(15[^4,\\D])|(17[678])|(18[0,0-9]))\\d{8}$";
    NSPredicate *phoneTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",phoneRegex];
    return [phoneTest evaluateWithObject:mobile];
    }
