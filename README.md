# Masked-Edittext
[ ![Download](https://api.bintray.com/packages/faogustavo/maven/MaskedEdittext/images/download.svg) ](https://bintray.com/faogustavo/maven/MaskedEdittext/_latestVersion) [![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Masked--Edittext-green.svg?style=true)](https://android-arsenal.com/details/1/3033) [![Android Gems](http://www.android-gems.com/badge/pinball83/Masked-Edittext.svg?branch=master)](http://www.android-gems.com/lib/pinball83/Masked-Edittext)
 
 Masked-Edittext android library EditText widget wrapper add masking and formatting input text functionality.
 
 ![Image phone number formatted input]
 (http://g.recordit.co/ROo3bzrX7k.gif)
 
 ![Image card number formatted input]
  (http://g.recordit.co/B8IuMTrsYi.gif)
 
# Install

##Maven

    <dependency>
      <groupId>com.gustavofao</groupId>
      <artifactId>masked-edittext</artifactId>
      <version>{version}</version>
      <type>pom</type>
    </dependency>

##Gradle

    compile 'com.gustavofao:masked-edittext:{version}'

**The {version} can be get from the badge**
    
#Usage
###Quick start
 You can choose using this widget thought declaring it in layout resource xml 
     
    <com.github.pinball83.maskededittext.MaskedEditText
                    android:id="@+id/masked_edit_text"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:inputType="number"
                    app:mask="8 (***) *** **-**"
                    app:notMaskedSymbol="*"
                    app:maskIcon="@drawable/abc_ic_clear_mtrl_alpha"
                    app:maskIconColor="@color/colorPrimary"
                    />

or programmatically create in source file
 
    MaskedEditText maskedEditText = new MaskedEditText(this,
                    "8 (***) *** **-**",
                    "*",
                    getResources().getDrawable(R.drawable.ic_account_circle),
                    new MaskedEditText.MaskIconCallback() {
                        @Override
                        public void onIconPushed() {
                            System.out.println("Icon pushed");
                            //Invoke here contact list or just clear input
                        }
                    });
  
###Attributes                        
MaskedEditText have following attributes 

####XML
    ...
    app:mask = "8 (***) *** **-**"                     //mask
    app:notMaskedSymbol = "*"                          //symbol for mapping allowed placeholders
    app:replacementChar = "#"                          //symbol which will be replaced notMasked symbol e.g. 8 (***) *** **-** will be 8 (###) ### ##-## by default it assign to whitespace
    app:deleteChar = "#"                               //symbol which will be replaced after deleting by default it assign to whitespace
    app:format = "[1][2][3] [4][5][6]-[7][8]-[10][9]"  //set format of returned data input into MaskedEditText
    app:maskIcon = "@drawable/abc_ic_clear_mtrl_alpha" //icon for additional functionality clean input or invoke additional screens
    app:maskIconColor = "@color/colorPrimary"          //icon tint color
    ...

####Java
Simple instance 

    MaskedEditText editText = new MaskedEditText(context, "8 (***) *** **-**", "*"); //set mask to "8 (***) *** **-**" and not masked symbol to "*"

text setup and formatting

    editText.setMaskedText("5551235567");                     //set text into widget it will be look like 8 (555) 123 55-67
    editText.setFormat("[1][2][3] [4][5][6]-[7][8]-[10][9]"); //set format of returned data input into MaskedEditText e.g editText.getUnmaskedText() return 8 (555) 123 55-76
     
Widget instance with mask, icon button and callback

    MaskedEditText maskedEditText = new MaskedEditText(this,
                "8 (***) *** **-**",
                "*",
                getResources().getDrawable(R.drawable.ic_account_circle),
                new MaskedEditText.MaskIconCallback() {
                    @Override
                    public void onIconPushed() {
                        System.out.println("Icon pushed");
                    }
                });

Getting text

    maskedEditText.getUnmaskedText() //return unmasked text
    maskedEditText.getText()         //return mask and text

####Validation
To use [Saripaar](https://github.com/ragunathjawahar/android-saripaar) validation, you first need to import the validation annotation.

```java
Validator.registerAnnotation(MaskedRequire.class);
```

Then you just need to use the MaskedRequire annotation on your object. The only required attribute is value. The others are optional.
```java
@MaskedRequire(
    value = "8 (***) *** **-**",
    complete = true,
    notMaskedSymbol = "\\*",
    replacementChar = ""
)
MaskedEditText maskedEditText;
```