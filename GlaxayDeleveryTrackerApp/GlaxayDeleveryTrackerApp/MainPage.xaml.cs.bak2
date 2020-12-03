using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

using Xamarin.Forms;
using Xamarin.Forms.Xaml;

namespace GlaxayDeleveryTrackerApp
{
    [XamlCompilation(XamlCompilationOptions.Compile)]
    public partial class MainPage : ContentPage
    {
        public String companyCode;
        public String trackNumber;
        public ClassState trackRstState;
        public string DbgMsg;

#if true
        String[] companyNametoCode = new String[]
        {
            "kr.cjlogistics",
            "kr.cupost",
            "kr.cvsnet",
            "kr.epost",
            "kr.hanjin",

            "kr.hdexp",
            "kr.homepick",
            "de.dhl",
            "us.fedex",
            "un.upu.ems",

            "us.ups",
            "us.usps",
            "kr.daesin",
            "kr.honamlogis",
            "kr.ilyanglogis",

            "kr.kdexp",
            "kr.kunyoung",
            "kr.logen",
            "kr.lotte",
            "kr.hanips",

            "jp.sagawa",
            "jp.yamato",
            "jp.yuubin",
            "kr.chunilps",
            "kr.cway",

            "kr.slx",
            "kr.swgexp",
            "nl.tnt",
        };
#else
        String[] companyNametoCode = new String[]
        {
            "de.dhl",
            "jp.sagawa",
            "jp.yamato",
            "jp.yuubin",
            "kr.chunilps",

            "kr.cjlogistics",
            "kr.cupost",
            "kr.cvsnet",
            "kr.cway",
            "kr.daesin",

            "kr.epost",
            "kr.hanips",
            "kr.hanjin",
            "kr.hdexp",
            "kr.homepick",

            "kr.honamlogis",
            "kr.ilyanglogis",
            "kr.kdexp",
            "kr.kunyoung",
            "kr.logen",

            "kr.lotte",
            "kr.slx",
            "kr.swgexp",
            "nl.tnt",
            "un.upu.ems",

            "us.fedex",
            "us.ups",
            "us.usps",
        };
#endif
        public MainPage()
        {
            InitializeComponent();
        }

        private async void bt_company_Clicked(object sender, EventArgs e)
        {
            await DisplayAlert("(c)FreeNanum", "freeNanum.github.io/market", "확인");
        }

        public void Picker_SelectedIndexChanged_deleivery(object sender, EventArgs e)
        {
            String localCompanyCode = companyNametoCode[pk1_company.SelectedIndex];

            if (pk1_company.SelectedIndex == -1)
            {
                companyCode = "";
            }
            else
            {
                companyCode = localCompanyCode;
            }
            //Console.WriteLine($"localCompanyCode: {localCompanyCode}");
        }

        // HttpClient is intended to be instantiated once per application, rather than per-use. See Remarks.
        static readonly HttpClient client = new HttpClient();
        static string responseBody;

#if false //Json sample structure.
{
   "from": {
      "name": "알*",
      "time": "2020-12-01T16:08:30+09:00"
   },
   "to": {
      "name": "박*",
      "time": null
   },
   "state": {
      "id": "out_for_delivery",
      "text": "배송출발"
   },
   "progresses": [
      {
         "time": "2020-12-01T16:08:30+09:00",
         "status": {
            "id": "at_pickup",
            "text": "상품인수"
         },
         "location": {
            "name": "서울한성"
         },
         "description": "보내시는 고객님으로부터 상품을 인수받았습니다"
      },
      {
        "time": "2020-12-01T20:22:22+09:00",
         "status": {
        "id": "in_transit",
            "text": "상품이동중"
         },
         "location": {
        "name": "강북"
         },
         "description": "물류터미널로 상품이 이동중입니다."
      },
      {
    "time": "2020-12-02T03:25:09+09:00",
         "status": {
        "id": "in_transit",
            "text": "상품이동중"
         },
         "location": {
        "name": "용인HUB"
         },
         "description": "배송지역으로 상품이 이동중입니다."
      },
      {
    "time": "2020-12-02T10:38:50+09:00",
         "status": {
        "id": "in_transit",
            "text": "상품이동중"
         },
         "location": {
        "name": "강동B"
         },
         "description": "고객님의 상품이 배송지에 도착하였습니다.(배송예정:이준표 010-6231-8055)"
      },
      {
    "time": "2020-12-02T12:54:04+09:00",
         "status": {
        "id": "out_for_delivery",
            "text": "배송출발"
         },
         "location": {
        "name": "서울강동길동"
         },
         "description": "고객님의 상품을 배송할 예정입니다.(16∼18시)(배송담당:이준표 010-6231-8055)"
      }
   ],
   "carrier": {
    "id": "kr.cjlogistics",
      "name": "CJ대한통운",
      "tel": "+8215881255"
   }
}
#endif
        public class ClassFrom
        {
            public string Name { get; set; }
            public string Time { get; set; }
        }

        public class ClassTo
        {
            public string Time { get; set; }
            public string Status { get; set; }

        }

        public class ClassState
        {
            public string Id { get; set; }
            public string Text { get; set; }
        }

       /* ------------------------------------------------------*/
        public class ClassStatus
        {
            public string Td { get; set; }
            public string Text { get; set; }
        }
        public class ClassLocation
        {
            public string Name { get; set; }
        }

        public class ClassProgresses
        {
            public string Time { get; set; }
            public ClassStatus Status { get; set; }
            public ClassLocation Location { get; set; }
            public string Description { get; set; }
        }

        /*-------------------------------------------------------*/
        public class ClassCarrier
        {
            public string Id { get; set; }
            public string Name { get; set; }
            public string Tel { get; set; }
        }

        public class JsonClassTrack
        {
            public ClassFrom From { get; set; }
            public ClassTo To { get; set; }
            public ClassState State { get; set; }
            public List<ClassProgresses> Progresses { get; set; }
            public ClassCarrier Carrier { get; set; }
        }

        /*------------------- 에러 메시지 -------------------------------------- */
        public class JsonClassMessage
        {
            public string Message { get; set; }
        }

#if FirstMethod
        public bool JsonParse(string responseBody)
        {
            JArray array = JArray.Parse(responseBody);
            foreach (JObject item in array.Children<JObject>())
            {
                //Console.WriteLine("AnimalId: " + item["message"]);
                if (!string.IsNullOrWhiteSpace(item["message"].ToString()))
                {
                    //DbgMsg = tMessage.Pmessage;
                    DbgMsg = string.Format("잘못된 운송장");
                    return false;
                }
#if false
                //Console.WriteLine("SpeciesCode: " + item["state"]);
                if (!string.IsNullOrWhiteSpace(item["state"].ToString()))
                {
                    //DbgMsg = string.Format("현재 배송 상태");
                    DbgMsg = item["state"].ToString();
                    return true;
                }
#endif



#if false

                //Console.WriteLine("SpeciesCode: " + item["state"]);
                if (!string.IsNullOrEmpty(item["state"].ToString()))
                {
                    JArray array2 = JArray.Parse(item["state"].ToString());
                    foreach (JObject item2 in array2.Children<JObject>())
                    {
                        DbgMsg = item2["text"].ToString();   //DbgMsg = string.Format("현재 배송 상태");
                        return true;
                    }
                }
#endif

#if false
                //Console.WriteLine("SpeciesCode: " + item["state"]);
                if (!string.IsNullOrEmpty(item["state"].Children().ToString()))
                {
                    JArray array2 = JArray.Parse(item["state"].Children().ToString());
                    foreach (JObject item2 in array2.Children<JObject>())
                    {
                        DbgMsg = item2["text"].ToString();   //DbgMsg = string.Format("현재 배송 상태");
                        return true;
                    }
                }
#endif
            }

#if false
            foreach (JObject item in array.Children<JObject>())
            {
                //Console.WriteLine("SpeciesCode: " + item["state"]);
                if (!string.IsNullOrEmpty(item["state"].ToString()))
                {
                    JArray array2 = JArray.Parse(item["state"].ToString());
                    foreach (JObject item2 in array2.Children<JObject>())
                    {
                        DbgMsg = item2["text"].ToString();   //DbgMsg = string.Format("현재 배송 상태");
                        return true;
                    }
                }
            }
#endif

            DbgMsg = string.Format("응답 오류");
            //DbgMsg = tmpSccsMessage;
            return false;

        }
#endif

#if SecondMethod
        public bool JsonParse(string responseBody)
        {


#if false// json내 모든 데이터를 파싱

                // Deseialize(JsonString -> Object)
                JsonClassMessage jsonCls = JsonConvert.DeserializeObject<JsonClassMessage>(responseBody);
                //Debug.WriteLine($"{jsonCls}");

                cMessage tMessage = jsonCls.jMessage;
#else // json내 일부 데이터를 파싱

            //JObject jObjErrMsg = JObject.Parse(responseBody);
            JObject jObj = JObject.Parse(responseBody);
            //JsonClassMessage tMessage = JsonConvert.DeserializeObject<JsonClassMessage>(jObjErrMsg.ToString());
            //DbgMsg = string.Format("디버그중1");
            
            string tmpMessage = (String)jObj["message"].ToString();
#endif
            //DbgMsg = string.Format("디버그중2");
            //DbgMsg = String.Format($"{tMessage.Pmessage}");
            //return false;

            //if (!string.IsNullOrEmpty(tMessage.Pmessage))
            if (!string.IsNullOrWhiteSpace(tmpMessage))
            {
                //DbgMsg = tMessage.Pmessage;
                DbgMsg = string.Format("잘못된 운송장");
                return false;
            }
            else
            {
                //DbgMsg = string.Format("운송장이 존재");

#if false // json내 모든 데이터를 파싱
                    // Deseialize(JsonString -> Object)
                    JsonClassTrack jsonCls = JsonConvert.DeserializeObject<JsonClassTrack>(responseBody);
                    //Debug.WriteLine($"{jsonCls}");

                    cFrom tFrom = jsonCls.JFrom;
                    cTo tTo = jsonCls.JTo;
                    cState tState = jsonCls.JState;
                    List<cProgresses> tProgresses = jsonCls.JProgresses;
                    cCarrier tCarrier = jsonCls.JCarrier;

#if JSON_SERIALIZE
                    // Serialize (Object -> JsonString)
                    string serRslt = JsonConvert.SerializeObject(jsonCls);
#endif

#else// json내 일부 데이터를 파싱
                // Desrialize (JsonStrin -> Object)
                //JObject jObj = JObject.Parse(responseBody);


                //cFrom tFrom = JsonConvert.DeserializeObject<cFrom>(jObj["from"].ToString());
                //cTo tTo = JsonConvert.DeserializeObject<cTo>(jObj["to"].ToString());
                //cState tState = JsonConvert.DeserializeObject<cState>(jObj["state"].ToString());
                //string tmpSccsMessage = (String)((jObj["state"]["text"]).ToString());

                //List<cProgresses> tProgresses = JsonConvert.DeserializeObject<List<cProgresses>>(jObj["progresses"].ToString());
                //cCarrier tCarrier = JsonConvert.DeserializeObject<cCarrier>(jObj["carrier"].ToString());

                //DbgMsg = string.Format("배송상태 확인 중");

#if JSON_SERIALIZE
                    // Serialize (Object -> JsonString)
                    string serRslt1 = JsonConvert.SerializeObject(tFrom);
                    string serRslt2 = JsonConvert.SerializeObject(tTo);
                    string serRslt3 = JsonConvert.SerializeObject(tState);
                    string serRslt4 = JsonConvert.SerializeObject(tProgresses);
                    string serRslt5 = JsonConvert.SerializeObject(tCarrier);
#endif

#endif

                //trackRstState = tState;
                DbgMsg = string.Format("배송상태 확인 완료");
                //DbgMsg = tmpSccsMessage;
                return true;

    }
#endif//#if SecondMethod

#if ThirdMethod
        public bool JsonParse(string responseBody)
        {
            JObject jo = JObject.Parse(responseBody);

            var Err = jo.SelectToken("message");
            if (!String.IsNullOrEmpty(Err.ToString())) //잘못된 운송장
            {
                DbgMsg = String.Format("잘못된 운송장");
                return false;
            }

            //배송상태
            var a = jo.SelectToken("state"); 
            var cnt = a.Count(); 
            
            if(cnt != 0) //배송 상태
            {
                foreach (var item in a)
                {
#if SAMPLE
                    //var key = item.SelectToken("key").ToString(); 
                    //var category = item.SelectToken("category").ToString(); 
                    //var text = item.SelectToken("text").ToString(); 
                    var items = item.SelectToken("items"); 
                    if (items != null) 
                    { 
                        foreach (var token in items) 
                        {
                            //var name = String.Format("{0}", token.SelectToken("name")); 
                            //var value = String.Format("{0}", token.SelectToken("value"));
                            //DbgMsg = String.Format("{0}", token.SelectToken("text"));
                        } 
                    } 
#endif
                    //배송 상태
                    DbgMsg = String.Format("{0}", item.SelectToken("text"));
                    return true;
                }
            }
            else //잘못된 운송장
            {
                DbgMsg = String.Format("잘못된 운송장");
                return false;
            }

            DbgMsg = String.Format("응답 파싱 오류");
            return false;
        }
#endif
        public bool JsonParse(string responseBody)
        {
            JObject jo = JObject.Parse(responseBody);

            var Err = jo.SelectToken("message");
            if (!String.IsNullOrEmpty(Err.ToString())) //잘못된 운송장
            {
                DbgMsg = String.Format("잘못된 운송장");
                return false;
            }

            //배송상태
            var a = jo.SelectToken("state").SelectToken("text");
            var Cnt = a.Count();

            if(Cnt != 0)
            {
                //배송 상태
                DbgMsg = String.Format("{0}", a.ToString());
                return true;
            }
            else
            {
                DbgMsg = String.Format("잘못된 운송장");
                return false;
            }
            
            DbgMsg = String.Format("응답 파싱 오류");
            return false;
        }

        public async Task<bool> Call_trackerDeiveryAPI()
        {
#if true
#if TEMP
            string address = "1400,Copenhagen,DK";
            string GoogleMapsAPIurl = "https://maps.googleapis.com/maps/api/geocode/json?address={0}&key={1}";
            string GoogleMapsAPIkey = "MYSECRETAPIKEY";
            string requestUri = string.Format(GoogleMapsAPIurl, address.Trim(), GoogleMapsAPIkey);
#endif

#if true
            string Carrier = companyCode;
            string TrackNumber = et_number.Text;
            string TrackAPIurl = "https://apis.tracker.delivery/carriers/{0}/tracks/{1}";
            string uriStr = string.Format(TrackAPIurl, Carrier.Trim(), TrackNumber.Trim());
#endif
#else

#if true
            String uriStr = "https://apis.tracker.delivery/carriers/" + companyCode +
                                                        "/tracks/" + et_number.Text;
#if false
                    Uri uriStr = new Uri(string.Format("https://apis.tracker.delivery/carriers/" + companyCode +
                                                            "/tracks/" + et_number.Text, string.Empty));
#endif
#else
                String uriStr = "https://apis.tracker.delivery/carriers/kr.cvsnet/tracks/11111";
#endif
#endif
            //Console.WriteLine($"API Url: {uriStr}");

            // Call asynchronous network methods in a try/catch block to handle exceptions.
            try
            {
#if true
                // Works fine                
                using (HttpResponseMessage response = await client.GetAsync(uriStr))
                {
                    DbgMsg = string.Format("HTTP Get Req.");
                    //if (response.IsSuccessStatusCode)
                    if(true)
                    {
                        DbgMsg = string.Format("Req Success.");
                        responseBody = response.Content.ReadAsStringAsync().Result;

                        DbgMsg = string.Format("Json parse.");
                        return JsonParse(responseBody);
                    }
                    else
                    {
                        DbgMsg = string.Format($"Req. Fail-{response.IsSuccessStatusCode}");
                        return false;
                    }
                }
                return false;

#if TEMP
                HttpResponseMessage response = await client.GetAsync(uriStr);
                DbgMsg = string.Format("HTTP Get Req.");
                if (response.IsSuccessStatusCode)
                {
                    DbgMsg = string.Format("Req Success.");

                    // Parse the response body. Blocking!
                    responseBody = await response.Content.ReadAsStringAsync();

                    DbgMsg = string.Format("Json parse.");
                    return JsonParse(responseBody);
                }
                DbgMsg = string.Format($"Req. Fail-{response.IsSuccessStatusCode}");
                //DbgMsg = string.Format("HTTP Req. Fail");
                return false;
#endif

#elif BlockingCall
                HttpResponseMessage response = client.GetAsync(uriStr).Result; //Blocking Call!
                DbgMsg = string.Format("HTTP Get Req.");
                if (response.IsSuccessStatusCode)
                {
                    DbgMsg = string.Format("Req Success.");

                    // Parse the response body. Blocking!
                    responseBody = response.Content.ReadAsStringAsync().Result;

                    DbgMsg = string.Format("Json parse.");
                    return JsonParse(responseBody);
                }
                DbgMsg = string.Format($"Req. Fail-{response.IsSuccessStatusCode}");
                //DbgMsg = string.Format("HTTP Req. Fail");
                return false;
#else
                HttpResponseMessage response = await client.GetAsync(uriStr);
                response.EnsureSuccessStatusCode();
                responseBody = await response.Content.ReadAsStringAsync();
                // Above three lines can be replaced with new helper method below
                string responseBody = await client.GetStringAsync(uriStr);

                return JsonParse(responseBody);
#endif
            }
            catch (HttpRequestException e)
            {
                //Console.WriteLine("\nException Caught!");
                //Console.WriteLine("Message :{0} ", e.Message);
                
                DbgMsg = string.Format("요청 에러가 발생");
                
                return false;
            }

        }

        public async void bt_search_Clicked(object sender, EventArgs e)
        {
                        
            if (String.IsNullOrWhiteSpace(companyCode))
            {
                await DisplayAlert("안내", "택배회사를 선택해주세요!", "확인");
                return;

            }
            else
            {
                //trackNumber = localTrackNumber;
            }

            //Console.WriteLine($"company-code: {companyCode}");

            if (String.IsNullOrWhiteSpace(et_number.Text))
            {
                await DisplayAlert("안내", "송장번호를 입력해주세요!", "확인");
                return;

            }
            else
            {
                trackNumber = et_number.Text;
            }
            //Console.WriteLine($"track_number: {trackNumber}");


            bool callRst = await Call_trackerDeiveryAPI();
            //bool callRst = Call_trackerDeiveryAPI();
            if (callRst == false)
            {
                //await DisplayAlert("안내", "해당 운송장이 존재하지 않습니다!", "확인");
                trackState.Text = DbgMsg;
            }
            else
            {
                //trackRstState = tmpTrackRst;
                //Console.WriteLine($"track_id: {trackRstState.id}" + $"track_text: {trackRstState.text}");
                
                //trackState.Text = trackRstState.Ptext;
                trackState.Text = DbgMsg;//"배송상태 확인 완료"
            }

        }//bt_search_Clicked()

        private bool IsNullOrEmpty(ClassState tmpTrackRst)
        {
            throw new NotImplementedException();
        }
    }
}