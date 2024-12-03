1. with后必须添加外键，不然会返回为空 

> 
$result=WorldBankRecord::with('region:iso2code')->where('date','2022')->where('iso2code', 'cn')->first();
$result=WorldBankRecord::with(['region:iso2code'])->where('date','2022')->where('iso2code', 'cn')->first();
= App\Models\WorldBank\WorldBankRecord {#7406
    id: 2302,
    iso2code: "CN",
    iso3code: "CHN",
    date: "2022",
    value: 1412175000.0,
    unit: "",
    obs_status: "",
    decimal: 0,
    world_bank_indicator_name: "SP.POP.TOTL",
    created_at: "2024-06-14 06:52:01",
    updated_at: "2024-06-14 06:52:01",
    region: App\Models\WorldBank\WoldBankCountryRegion {#7431
      iso2code: "CN",
    },
  }


2. 上面返回了对象， 现在需要返回指定的字段。
2.1  增加belongsTo还是不起作用。 
2.1.1 增加belongsTo
    return $this->belongsTo(WoldBankCountryRegion::class,'iso2code','iso2code')->select(array('iso2code','iso3code','region_name','region_name_cn'));
2.1.2 
> $result=WorldBankRecord::with(['region:iso2code'])->where('date','2022')->where('iso2code', 'cn')->first();
= App\Models\WorldBank\WorldBankRecord {#7436
    id: 2302,
    iso2code: "CN",
    iso3code: "CHN",
    date: "2022",
    value: 1412175000.0,
    unit: "",
    obs_status: "",
    decimal: 0,
    world_bank_indicator_name: "SP.POP.TOTL",
    created_at: "2024-06-14 06:52:01",
    updated_at: "2024-06-14 06:52:01",
    region: App\Models\WorldBank\WoldBankCountryRegion {#7416
      iso2code: "CN",
    },
  }

2.2 增加query 指定返回值
2.2.1 不行 

$result=WorldBankRecord::with(['region:iso2code'=> function ($query) { $query->select('iso2code', 'iso3code');}])->where('date','2022')->where('iso2code', 'cn')->first();
 Call to undefined relationship [region:iso2code] on model [App\Models\WorldBank\WorldBankRecord].


2.3 删除 外键。居然行了。

$result=WorldBankRecord::with(['region'=> function ($query) { $query->select('iso2code', 'iso3code'，'region_name');}])->where('date','2022')->where('iso2code', 'cn')->first();


2.4 直接用， 居然也行了。
> $result=WorldBankRecord::with(['region'])->where('date','2022')->where('iso2code', 'cn')->first();
= App\Models\WorldBank\WorldBankRecord {#7443
    id: 2302,
    iso2code: "CN",
    iso3code: "CHN",
    date: "2022",
    value: 1412175000.0,
    unit: "",
    obs_status: "",
    decimal: 0,
    world_bank_indicator_name: "SP.POP.TOTL",
    created_at: "2024-06-14 06:52:01",
    updated_at: "2024-06-14 06:52:01",
    region: App\Models\WorldBank\WoldBankCountryRegion {#7449
      iso2code: "CN",
      iso3code: "CHN",
      region_name: "China",
      region_name_cn: "中国",
    },
  }

2.5 删除belongsTo后面的select。 $result=WorldBankRecord::with(['region'])->where('date','2022')->where('iso2code', 'cn')->first();  又不行了。



所以真正起作用的时belongsTo 后面的select



