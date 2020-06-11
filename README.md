# Reading Nonstandard 1D Barcode
The sample demonstrates how to use [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/Products/Dynamic-Barcode-Reader.aspx) to decode nonstandard 1D barcode.

## Environment
Python 3.x

## Install Dynamsoft Barcode Reader

```bash
pip install dbr
```

## Usage

Get a [free trial license](https://www.dynamsoft.com/CustomerPortal/Portal/Triallicense.aspx) and then update following code:

```python
license_key = "LICENSE-KEY" 
```

Configure the template JSON file. Set the barcode format and start/stop characters. Here is an example for [Code39](https://en.wikipedia.org/wiki/Code_39):

```
"StandardFormat": "BF_CODE_39",
"HeadModuleRatio": "131111313",
"TailModuleRatio": "131111313"
```

According to the [character table](https://en.wikipedia.org/wiki/File:Free_3_of_9_(Code_39_barcode).svg), "`131113131`" represents "`+`" and "`131111313`" represents "`-`".

Once the template file is correctly configured, you can read the nonstandard 1D barcode as follows:

```python
reader = BarcodeReader()
reader.init_license(license_key)

error = reader.init_runtime_settings_with_file(json_file)
if error[0] != EnumErrorCode.DBR_OK:
    print(error[1])

try:
    text_results = reader.decode_file(filename)
    if text_results != None:
        for text_result in text_results:
            print('Barcode Format:')
            print(text_result.barcode_format_string_2)
            print('')
            print('Barcode Text:')
            print(text_result.barcode_text)
            print('')
            print('Localization Points:')
            print(text_result.localization_result.localization_points)
            print('------------------------------------------------')
            print('')
except BarcodeReaderError as bre:
    print(bre)

```