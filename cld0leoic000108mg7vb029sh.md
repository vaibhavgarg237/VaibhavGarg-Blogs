---
title: "Let's Parse stringified JSON in C++"
seoTitle: "Parse JSON in C++"
seoDescription: "Learn how to easily parse JSON in C++ using JSONCPP. In this blog post, we walk you through the process of using this powerful library to parse JSON data."
datePublished: Tue Jan 17 2023 18:52:53 GMT+0000 (Coordinated Universal Time)
cuid: cld0leoic000108mg7vb029sh
slug: parse-json-cpp
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1673981123060/750a6ebc-d3ea-4455-bbba-de6d284275af.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1673981313108/5977a48d-1ca7-4769-8109-606ed916464a.png
tags: cpp, c, javascript, json-parser, string-methods

---

Let's agree that JSON is meant to be extracted using Javascript. Yes! Because its full form is Javascript object notation.😅😂 But we should also agree that it's a lightweight data-interchange format that can exchange data between different programming languages and platforms. Actually, it is a language-independent data format. But if we want the speed of C++ and the magic of JSON we need to learn how we can extract data from JSON in C++. I would be very honest with you, it's sometimes really painful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673980765793/47f7265d-f3c1-42c3-b1e7-7e6453d90f40.png align="center")

In this article, we will learn to parse JSON using **JsonCPP**. You can also use other libraries like RapidJSON or nlohmann. It becomes quite convenient once you use it. But TBH parsing in Javascript is super easy as we just need a single dot (.) / \[ \] / simple methods to access its members or even optional chaining to avoid any further duck ups!

1. Install jsoncpp library
    
    ```bash
    git clone https://github.com/open-source-parsers/jsoncpp
    cd jsoncpp
    python amalgamate.py
    ```
    
    The above commands will generate the include and dist folder, now you can copy them to your project folder and include them in your project accordingly. Alternatively, you can also use CMakeList or directly include in your build command to include the include and library paths. This is basically to use `#include <jsoncpp/json/json.h>` and `#include <json/json.h>` in our C++ code.
    
2. Finally, we can now Parse our JSON
    
    ```cpp
    #include <iostream>
    #include <jsoncpp/json/json.h>
    #include <json/json.h>
    #include <string>
    using namespace std;
    
    int main()
    {
      std::string inputJSON = "{\"nameOne\":\"Jayant Sharma\",\"nameTwo\":Jyoti Verma,\"city\":\"New York\"}";
    
      Json::Value outputDataAsJson;
      Json::CharReaderBuilder readerBuilder;
      std::string err;
      const std::unique_ptr<Json::CharReader> reader(readerBuilder.newCharReader());
    
      std::string name1, name2, city;
      if (reader->parse(inputJSON.c_str(), inputJSON.c_str() + inputJSON.length(), &outputDataAsJson, &err))
      {
        name1 = outputDataAsJson["nameOne"].asString();
        name2 = outputDataAsJson["nameTwo"].asString();
        city = outputDataAsJson["city"].asString();
      }
      else
      {
        cout << "Some error occurred" << endl;
      }
    
      cout << "value of key:Name1 in JSON" << name1 << endl;
      cout << "value of key:Name2 in JSON" << name2 << endl;
      cout << "value of key:city in JSON" << city << endl;
    }
    ```
    

In the above example, inputJson is a stringified JSON. On calling the parsing method on the reader with inputJson as a parameter it stores parsed JSON inside outputDataAsJson. Now we can easily fetch our values from this format.  
Here `Json::Value`, `Json::CharReaderBuilder` & `Json::CharReader` are from the JsonCpp library.  
This example uses the `Json::Value` and `Json::Reader` classes from the JsonCpp library. The `Json::Value` class is used to represent JSON values and the `Json::Reader` class is used to parse a JSON string and create a `Json::Value` object.

It is necessary to use these methods `asString()`, `asInt()`, `asDouble()`, etc. to get the value of the JSON element `outputDataAsJson["nameOne"]` and also use the `[]` operator to access the child element of a JSON object.

On similar lines, we can extract data from our stringified JSON. There are also other ways to do this but this was a simplistic way. If you have a better solution you can comment below your solution so as to help other readers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673980472857/fed56b86-0572-4620-99ff-6f41cc0d1448.png align="center")