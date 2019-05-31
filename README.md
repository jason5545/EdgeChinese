# EdgeChineseTW
新版edge正體中文化工具 參照微軟官方語言資源庫進行製作

# 依賴
pak_tools.exe (pak_tools \[mac版] ) 可以解包打包pak檔案，shuax寫的

python3

# 原理
使用詞典，翻譯英文到正體中文。

# 使用

*特別注意，不同版本pak不通用！即使是同一個版本的64位元和32位元也不通用！所以每個版本都要重新產生*
*建議使用最新版的chromium中的語言檔案(pak)檔案*
*Mac和Windows的語言檔案可能不通用*

## 解釋
為了避免全部手動翻譯，我最開始用了chrome金絲雀的資源來製作詞典。 

##### Windows系統
1. 將chromium中的Locales下面的en-US.pak和zh-TW.pak複製到chrome目錄下,覆蓋已有檔案
2. 進入chrome目錄，使用unpack.bat解包en-us.pak，zh-TW.pak為en-US.json，zh-TW.json
    + 同時會執行dict.py並會產生en_cn_dict.json這個詞典檔案
3. 將Edge中Locales下面的en-US.pak放到專案根目錄    
4. 執行build.bat得到zh-TW.pak
5. (選擇性) 可在manual.json中補全一些存在於not_translate.json中的未翻譯的內容
6. (選擇性) 再次執行build.bat產生zh-TW.pak
7. 將產生的zh-TW.pak放回到Locales下面即可得到正體中文化版本
    + 如果不行就把原始的en-us.pak刪掉。

##### Mac系統

*此處測試是macOS X 10.14.4,由於安裝了python2和python3,因此sh命令用python3來執行py檔案,這點請注意*
*類似 /Contents/ 的路徑省略了一段, 直接在Finder中打開左側 應用程式 目錄,在App上按一下滑鼠右鍵->顯示套件內容即進入到該目錄前置目錄*
1. 將chromium中 /Contents/Versions/版本號碼/XXXX.framework/Versions/A/Resources 下的en.lproj,zh_TW.lproj這兩個資料夾複製到chrome目錄下,覆蓋已有檔案
    + XXXX根據你使用的是chrome還是chromium,可能會不一樣
2. 進入chrome目錄,使用unpack.sh解包語言包,解包後的json檔案在各自的資料夾下
    + 注意:需要設定sh檔案的打開方式為終端(sh檔案上右鍵->打開方式->其他->選擇終端(要修改啟用為 啟用\:所有應用程式 )->確定)
    + 同時會執行dict.py並會產生en_cn_dict.json這個詞典檔案
3. 將Edge中 /Contents/Versions/版本號碼/Microsoft Edge Framework.framework/Versions/A/Resources 下的en.lproj資料夾複製到專案根目錄
4. 按兩下build.sh得到zh_TW.lproj資料夾
5. (選擇性) 可在manual.json中補全一些存在於not_translate.json中的未翻譯的內容
6. (選擇性) 再次執行build.sh產生zh_TW.lproj資料夾
7. 將產生的zh_TW.lproj資料夾放到 /Contents/Versions/版本號碼/Microsoft Edge Framework.framework/Versions/A/Resources 下
8. (若已經處理過,則無須此操作) 修改 mac版專用/zh_TW.lproj/InfoPlist.strings文件,修改方法見 mac版專用/說明.txt文件
9. (若已經處理過,則無須此操作) 將修改好的 mac版專用/zh_TW.lproj 資料夾放回到 /Contents/Resources

---

translate.py會根據詞典en_cn_dict.json自動的把en-US.json翻譯成zh-TW.json。

因為詞典不會100%全，所以準備了一個手動詞典manual.json，可以手動翻譯不全的部分。

經過多次修改以後，詞典就會越來越全。

未翻譯部分會寫入not_translate.json，方便查看翻譯有多少缺失。

放入最新版edge的en-us.pak(en.lproj/locale.pak)，執行build.bat(build.sh)會執行三個動作。

1. 解包en-us.pak(en.lproj/locale.pak)為en-us.json(en.lproj/locale.json)
2. 調用translate.py把en-us.json(en.lproj/locale.json)正體中文化為zh-TW.json(zh_TW.lproj/locale.json)
3. 打包zh-TW.json(zh_TW.lproj/locale.json)成zh-TW.pak(zh_TW.lproj/locale.pak)

# 致謝
[shuax/EdgeChinese](https://github.com/shuax/EdgeChinese)
