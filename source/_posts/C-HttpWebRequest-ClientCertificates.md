---
title: 'C# HttpWebRequest ClientCertificates'
date: 2019-03-19 20:00:14
categories:
- HttpWebRequest
tags:
- HttpWebRequest
- C#
- 筆記
---

# C# HttpWebRequest ClientCertificates

````C#

byte[] aryData = Encoding.UTF8.GetBytes(string.Empty);

            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create("URL");

            //// 設定私有憑證
            req.ClientCertificates.Add(new X509Certificate(HttpRuntime.AppDomainAppPath + @"\yourCertificates.p12", "yourpassword"));
            X509Store certStore = new X509Store("My", StoreLocation.LocalMachine);
            certStore.Open(OpenFlags.ReadOnly | OpenFlags.OpenExistingOnly);
            X509Certificate2 cert = certStore.Certificates[0];
            certStore.Close();
            req.ClientCertificates.Add(cert);

            req.Method = "POST";
            req.ContentType = "application/json";
            req.ContentLength = aryData.Length;
            req.Accept = "application/json";

            using (Stream reqStream = req.GetRequestStream())
            {
                reqStream.Write(aryData, 0, aryData.Length);
            }

            string strResult = string.Empty;

            using (WebResponse res = req.GetResponse())
            {
                using (Stream resStream = res.GetResponseStream())
                {
                    using (StreamReader objSR = new StreamReader(resStream))
                    {
                        strResult = objSR.ReadToEnd();
                    }
                }
            }

            return strResult;

````

# 參考

* [Force HttpWebRequest to send client certificate](https://stackoverflow.com/questions/39528973/force-httpwebrequest-to-send-client-certificate)