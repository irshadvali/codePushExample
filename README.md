1-  react-native init codePushExample
2- npm install react-native-code-push 
3- react-native link

4- npm install -g code-push-cli
5-code-push register
   then you will get one Webkey
 4Enter your token from the browser:  b344e9faff58ecb5f5e41904d65d2b2cde80e381
6-Then add the app to code-push followed with app name with respect to the platform you wanted (Android/iOS) 


(A)  Android 

code-push app add codePushExample-Android android react-native 

Then get Deployment Key    
(i) Production key  (ii) Staging Key




(B) iOS 
code-push app add codePushExample-Ios ios react-native 






code-push app add codePushExample-Android android react-native 

┌────────────┬──────────────────────────────────────────────────────────────────┐
│ Name       │ Deployment Key                                                   │
├────────────┼──────────────────────────────────────────────────────────────────┤
│ Production │ z4gK760K2V3PDhkyrNTfyXs-GrtR4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6 │
├────────────┼──────────────────────────────────────────────────────────────────┤
│ Staging    │ WLL2FLbQAt2_cC4_BDvYLDtE05Fv4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6 │



code-push app add codePushExample-Ios ios react-native 


┌────────────┬──────────────────────────────────────────────────────────────────┐
│ Name       │ Deployment Key                                                   │
├────────────┼──────────────────────────────────────────────────────────────────┤
│ Production │ r4q1wDxhjU_Jh_Jj5iJJxWBdWSbn4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6 │
├────────────┼──────────────────────────────────────────────────────────────────┤
│ Staging    │ dN80NgXIuk-_QgElIbC3e5bkg02D4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6 │
└────────────┴──────────────────────────────────────────────────────────────────┘

in android-  MainApplication


Below Green color code add in your MainApplication.java file 


public class MainApplication extends Application implements ReactApplication {
  private final String staging_React_Native_Key = "WLL2FLbQAt2_cC4_BDvYLDtE05Fv4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6";

  private final String production_React_Native_Key = "z4gK760K2V3PDhkyrNTfyXs-GrtR4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6";
  private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {

        @Override
        protected String getJSBundleFile() {
        return CodePush.getJSBundleFile();
        }
    
    @Override
    public boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
            new CodePush(staging_React_Native_Key, MainApplication.this, BuildConfig.DEBUG)
      );
    }

    @Override
    protected String getJSMainModuleName() {
      return "index";
    }
  };

  @Override
  public ReactNativeHost getReactNativeHost() {
    return mReactNativeHost;
  }

  @Override
  public void onCreate() {
    super.onCreate();
    SoLoader.init(this, /* native exopackage */ false);
  }
}



IOS- Info.plist

 <key>CodePushDeploymentKey</key>
    <string>dN80NgXIuk-_QgElIbC3e5bkg02D4d40d29b-d7a5-4ccd-ab5a-d16cda9561e6</string>
  </dict>

In App.js Or Index.js (Which is first Js file launch in your app )


Add below code :
import codePush from "react-native-code-push";

  componentDidMount() {
    codePush.sync({
      updateDialog: true,
      installMode: codePush.InstallMode.IMMEDIATE
    });
    console.disableYellowBox = true;
  }


For code pushon server you have to run below command

Android:

 code-push release-react codePushExample android

code-push promote codePushExample Staging Production

IOS:

 code-push release-react codePushExampleIos Ios

code-push promote codePushExampleIos Staging Production





To see the keys
code-push deployment list react-native-todo -k