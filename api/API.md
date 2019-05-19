# ����play ��Զ�̷��ʡ� API

## ����

����play��Զ�̷��ʡ������ܹ��õ�����appͨ��wifi���ӵ�PC�ϵĵ���play����������ͨ��http restful api�����Ʋ������Ĳ��ţ����ǲ鿴��ǰ�����뵯Ļ�����ݣ���������ֱ�Ӵ�������PC�ϵ���Ƶ�ļ���

## ԭ��

����play��Զ�̷��ʡ��������ڵ���play��for Windows/UWP�ͻ��ˣ��д��һ��С�͵�http webӦ�÷������������������ڲ���صĹ��ܺ�������RESTful API�ӿڵ���ʽ��¶�ھ������С�Ҳ����˵������play����������һ���ͻ��ˣ�����ڵ���play���������ԣ�������һ���������ˣ����������Ӧ�ã���

## ��ַ��˿�

Ĭ������£�����play���������������IP�� `80` �˿ڣ��û������޸Ĵ������á����豾��IPΪ `192.168.31.100`����ô���Ӧ�������ͨ�� `http://192.168.31.100:80` ���ӵ�����play��Զ�̷��ʡ�����

�����ǰ�����й���IP������������Ҳ����ͨ���������з��ʣ����� `http://www.xxxxx.com:80`

## URL

Զ�̷���APIΪ�˷���ʹ���뿪�������нӿڶ��� `/api/v1` ��ͷ�����Ҷ�����ֱ��ͨ��HTTP `GET` ���������ʵ���
����ĳЩ��ȡ���ݵ����͵��������⣬�ͻ����ڷ����������Ҫ�жϷ������Լ������Ƿ�ɹ���ɡ�
�����б��У�URL���������ŵı�ʾ�˴�Ϊ���������� `{hash}` ��ʾ�ڷ������APIʱ��Ҫ�� `{hash}` �滻Ϊ�����Ĳ���ֵ��

����API��֧��CORS��

## API��Կ��֤

��9.0�濪ʼ��Զ�̷���֧��ʹ����Կ��API���м��ܡ�����û�����������ã�����Ӧ���ڷ���ʱ��Ҫ�ṩ��Ӧ����Կ�ſ��������������ݣ�����᷵��http 401����ͨ����֤�ķ�ʽ��������ʹ�����з������е�һ�ּ��ɣ�
�������û������� abcde ��ΪAPI��Կ�� 

- ��http header���Authorizationͷ������: 
  - **Authorization: Bearer** abcdefgh
- ��url�����б�������token���������磺
  - /api/v1/control/volume/99?**token=abcde**
  - /api/v1/download/tasks/1122-3344-5566/?remove=1&**token=abcde**

 ����ͨ�� `/api/v1/welcome` �ӿڷ��ص� `tokenRequired` �������жϵ�ǰ�û��Ƿ�������Կ��֤��

# API�б�

## 1.��ȡ��ӭ��Ϣ�� /api/v1/welcome �� /welcome

### ��������֤

����API��Կ���ɵ��á�

### ����ֵ

```json
{
  "message": "Hello dandanplay user!",
  "version": "9.4.7.517",
  "time": "05/19/2019 11:45:45",
  "tokenRequired": true
}
```

### ����ֵ˵��

- version������play��ǰ�İ汾�ţ�����ͨ����ֵ�ж�ĳЩapi�Ƿ���ڡ�
- time����ǰ���е���play�������ı���ʱ�䡣
- tokenRequired����ʾ��ǰ�Ƿ�����API��֤���������Ϊ `true`������ʱ��Ҫ������Կ����������Ϸ���API��֤��һ�ڡ�

## 2.���Ʋ������������� /api/v1/control/volume/{volume}

### ����

- volume����������Χ0-100

## 3.���Ʋ�������ת���� /api/v1/control/seek/{time}

### ����

- time����������Χ0-max����λΪ���룬���紫�� 12345������Ƶ��ת����12.345�봦

## 4.���Ʋ�������ǰ�Ĳ���״̬ /api/v1/control/{method}

### ����

- method������ȡֵ֮һ���ֱ���� ���š�ֹͣ����ͣ����һ����Ƶ����һ����Ƶ
  - play
  - stop
  - pause
  - next
  - previous

## 5.��ȡ��ǰ���ڲ��ŵ���Ƶ��Ϣ /api/v1/current/video

### ����ֵ

```json
{
  "EpisodeId": "136290001",
  "AnimeTitle": "���ܻ�ӭ��֮��",
  "EpisodeTitle": "��1�� ��ޥ�ƥ��å��������",
  "Duration": 720052,
  "Position": 0.455077559,
  "Seekable": true,
  "Volume": 100,
  "Playing": true
}
```

### ����ֵ˵��

- EpisodeId����Ļ���ţ���ֵΪ�ַ�����ʽ�����ҿ���Ϊ`null`
- AnimeTitle��������
- EpisodeTitle���ӱ���
- Duration����Ƶ���ȣ����룩������ֵ�������������ת������apiʹ��
- Position����ǰ���ȣ���Χ0-1
- Seekable����ǰ��Ƶ�Ƿ�֧����ת���ȣ�������ý����Ƶ��ֱ����Ƶ��֧����ת
- Volume����ǰ������������С����Χ0-100

## 6.��ȡ��ǰ��Ƶ�ĵ�Ļ�б� /api/v1/current/comment

### ����ֵ��ʼ��Ϊxml��ʽ��

```xml
<?xml version="1.0"?>
<ArrayOfVisualDmItem xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <VisualDmItem ID="6216430746861568" UserID="[BiliBili]a74890bc" Time="36.126" Mode="Normal" Color="16777215" Size="25" Timestamp="1538999075" Pool="0">ûʲô ����</VisualDmItem>
  <VisualDmItem ID="6216455581335554" UserID="[BiliBili]ac3e8e82" Time="339.338" Mode="Normal" Color="16777215" Size="25" Timestamp="1538999123" Pool="0">��̨��̫������</VisualDmItem>
  <VisualDmItem ID="6216487250952192" UserID="[BiliBili]6c718d25" Time="630.841" Mode="Normal" Color="16777215" Size="25" Timestamp="1538999183" Pool="0">���ĵ���Ч</VisualDmItem>
</ArrayOfVisualDmItem>
```

## 7.��ȡ��ǰ�����б����� /api/v1/playlist

### ����ֵ

```json
[
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[01][GB_MP4][1280X720].mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[02][GB_MP4][1280X720]V2.mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[03][GB_MP4][1280X720].mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[04][GB_MP4][1280X720].mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[05][GB_MP4][1280X720].mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[06][GB_MP4][1280X720].mp4",
  "Y:\\���ܻ�ӭ��֮��\\[HYSUB]Himote House[07][GB_MP4][1280X720].mp4"
]
```

### ����ֵ˵��

�ַ����б�����Ϊ��Ƶ�ڱ���Ӳ���ϵ�����·����

## 8.��ȡý����е��������� /api/v1/library

### ����ֵ

```json
[
  {
    "AnimeId": 14198,
    "EpisodeId": 141980003,
    "AnimeTitle": "����ż���Ǵ���",
    "EpisodeTitle": "��3�� DEAD OR LIVE SAGA",
    "Id": "c004e475-d9bb-41e1-976b-7fce00997f3a",
    "Hash": "03778309A0E8A09C2F43603A490F2E98",
    "Name": "[Zombieland Saga][03][BIG5][1080P].mp4",
    "Path": "Y:\\[Zombieland Saga][03][BIG5][1080P].mp4",
    "Size": 518754774,
    "Rate": 0,
    "IsStandalone": false,
    "Created": "2018-10-21T23:14:59",
    "LastMatch": "0001-01-01T00:00:00",
    "LastPlay": "2019-04-25T18:00:22",
    "LastThumbnail": "2019-03-05T22:03:20",
    "Duration": 1420
  },
  {
    "AnimeId": 11167,
    "EpisodeId": 111670021,
    "AnimeTitle": "����ʯ֮�� 0",
    "EpisodeTitle": "��21�� �Y��Υ�ʥ����� Return of Phoenix",
    "Id": "686b4d07-d8de-4f2e-b716-3cf0843cc903",
    "Hash": "334763177A0B9A5647B263AA74E0A013",
    "Name": "[Nekomoe kissaten][Steins;Gate 0][21][GB][720P].mp4",
    "Path": "Y:\\[Nekomoe kissaten][Steins;Gate 0][21][GB][720P].mp4",
    "Size": 128023969,
    "Rate": 0,
    "IsStandalone": false,
    "Created": "2018-09-23T23:30:38",
    "LastMatch": "0001-01-01T00:00:00",
    "LastPlay": null,
    "LastThumbnail": "2019-03-05T22:03:22",
    "Duration": 1420
  },
  {
    "AnimeId": 13031,
    "EpisodeId": 130310010,
    "AnimeTitle": "Princess Principal",
    "EpisodeTitle": "��10�� Comfort Comrade",
    "Id": "07c0d08a-6191-49aa-866c-5ea91cf91f23",
    "Hash": "432A9EC48627FFA2F092B418840A5D98",
    "Name": "[HYSUB]Princess Principal[10][GB_MP4][1280X720].mp4",
    "Path": "Y:\\Princess Principal\\[HYSUB]Princess Principal[10][GB_MP4][1280X720].mp4",
    "Size": 158818535,
    "Rate": 0,
    "IsStandalone": false,
    "Created": "2017-10-08T17:09:31",
    "LastMatch": "0001-01-01T00:00:00",
    "LastPlay": null,
    "LastThumbnail": "2019-03-05T22:03:23",
    "Duration": 1470
  }
]
```

### ����ֵ˵��

һ����Ƶ��Ϣ���б�

- Id����Ƶ��Ψһ��ţ�GUID��ʽ
- AnimeId��������ţ�������ͬ��������Ƶ����ͬ���Ķ������
- EpisodeId����Ļ����
- AnimeTitle��������
- EpisodeTitle���ӱ���
- Hash������Ƶ�������루��Ҫ��
- Name������Ƶ���ļ�����ȥ��·����Ϣ��
- Path������Ƶ��Ӳ���ϵ�����·��
- Size���ļ��������λΪByte
- Rate���û��Դ���Ƶ���ݵĴ�֣�Ŀǰȫ��Ϊ0
- Created������playý�����¼����Ƶ��ʱ��
- LastPlay���ϴ�ʹ�õ���play���Ŵ���Ƶ��ʱ��
- Duration����Ƶʱ������λΪ��
- LastThumbnail���ϴ���������ͼ��ʱ��
- IsStandalone���Ƿ�Ϊ�����ļ�������������ý�������ļ����ڵ��ļ�

## 9.��ȡ��Ƶ����ͼ /api/v1/image/{hash} �� /api/v1/image/id/{id}

### ����

- hash����Ƶ������
- id����Ƶ���

### ����ֵ

jpeg��ʽ��ͼƬ�ļ�

## 10.���Ʋ����������ļ� /api/v1/load/{hash} �� /api/v1/load/id/{id}

### ����

- hash����Ƶ������
- id����Ƶ���

### ��ע

��ʹ�� `hash` ���������ļ�ʱ������ж����ͬhash����Ƶ������һ����Ƶ�������˶���ط�����������������е�һ����

## 11.��ȡָ����Ƶ�ĵ�Ļ/api/v1/comment/{hash} �� /api/v1/comment/id/{id}

### ����

- hash����Ƶ������
- id����Ƶ���

### ����ֵ��ʼ��Ϊxml��ʽ��

```xml
<?xml version="1.0"?>
<i xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <chatserver>chat.bilibili.com</chatserver>
  <chatid>10000</chatid>
  <mission>0</mission>
  <maxlimit>8000</maxlimit>
  <source>e-r</source>
  <ds>931869000</ds>
  <de>937654881</de>
  <max_count>8000</max_count>
  <d p="37.26,1,25,16777215,1500358682,0,0,0">����֮��</d>
  <d p="1419.41,1,25,16777215,1500459905,0,0,0">�Թź���������</d>
  <d p="825.54,1,25,16777215,1500479598,0,0,0">��������������Ұ���ٵ�Ů���Ǻò���</d>
  <d p="451.43,1,25,16777215,1500654750,0,0,0">����JK�������磿</d>
  <d p="787646,5,25,16777215,1500746390,0,0,0">������</d>
  <d p="1370.48,1,25,16777215,1500823550,0,0,0">���ED�뵽����</d>
  <d p="1043153,1,25,16777215,1500998696,0,0,0">cm�ȿ�������</d>
  <d p="1402.12,1,25,16777215,1501421432,0,0,0">�۸в���</d>
  <d p="138.36,1,25,16777215,1501592568,0,0,0">ҩЧ����������</d>
  <d p="1220.78,1,25,16777215,1501595590,0,0,0">û����������������������֮��Ϊɶ�ָ�������</d>
  <d p="333.23,1,25,16777215,1502119367,0,0,0">��ʶ���ӵ���ʵ�򲻴���̥</d>
</i>
```

### ��ע

���ظ�ʽ��BiliBili�ĵ�Ļ��ʽ��ͬ����������������play��������ȡ���µĵ�Ļ�����Է��ʴ�apiʱ���ܾܺòŻ᷵�ص�Ļ��

## 12.������Ƶ /api/v1/stream/{hash} �� /api/v1/stream/id/{id}

### ����

- hash����Ƶ������
- id����Ƶ���

### ����ֵ

��Ƶ�ļ�����֧�� range������ֱ����������в��š�

## 13.��ȡ���������б� /api/v1/download/tasks

### ����ֵ

��ǰ��������������б�

```json
[
  {
    "Id": "9CF5D1F0A923B423848327F6AC533C72EFF37192",
    "Progress": 1,
    "IsDownloadFinished": true,
    "Title": "[DMG&MH][Shoujo Kageki Revue Starlight][12 END][720P][GB].mp4",
    "State": 6,
    "StateText": "Stopped",
    "TotalBytes": 124095425,
    "DownloadedBytes": 124095425,
    "DownloadSpeed": 0,
    "UploadSpeed": 0,
    "RemainTime": 0,
    "SavePath": "Y:\\��Ů���",
    "Ignore": "",
    "CreatedTime": "2018-10-08T23:09:35.724706+08:00",
    "FirstFinishTime": null,
    "UpdatedTime": null,
    "EnableAcceleration": true,
    "EnteredAcceleration": false,
    "IsDeleted": false,
    "LazyLoad": true,
    "Files": [
      {
        "FileIndex": 0,
        "FileName": "[DMG&MH][Shoujo Kageki Revue Starlight][12 END][720P][GB].mp4",
        "FilePath": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][12 END][720P][GB].mp4",
        "Progress": 1,
        "FileSize": 124095425
      }
    ],
    "ContainingFolder": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][12 END][720P][GB].mp4"
  },
  {
    "Id": "A6A3CE0BB1F34752D349ABB5AEFFA2693A631178",
    "Progress": 1,
    "IsDownloadFinished": true,
    "Title": "[DMG&MH][Shoujo Kageki Revue Starlight][01][720P][GB].mp4",
    "State": 6,
    "StateText": "Stopped",
    "TotalBytes": 171046271,
    "DownloadedBytes": 171046271,
    "DownloadSpeed": 0,
    "UploadSpeed": 0,
    "RemainTime": 0,
    "SavePath": "Y:\\��Ů���",
    "Ignore": "",
    "CreatedTime": "2018-09-07T12:06:23.7257195+08:00",
    "FirstFinishTime": null,
    "UpdatedTime": null,
    "EnableAcceleration": true,
    "EnteredAcceleration": false,
    "IsDeleted": false,
    "LazyLoad": true,
    "Files": [
      {
        "FileIndex": 0,
        "FileName": "[DMG&MH][Shoujo Kageki Revue Starlight][01][720P][GB].mp4",
        "FilePath": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][01][720P][GB].mp4",
        "Progress": 1,
        "FileSize": 171046271
      }
    ],
    "ContainingFolder": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][01][720P][GB].mp4"
  }
]
```

### ����ֵ˵��

- Id����������ID����BT Hash
- Progress�����ؽ��ȣ���Χ��0.0-1.0������ͨ���������ж�����״̬��С��1.0Ϊδ��ɣ����ڵ���1.0Ϊ�����
- Title�������������
- State���������ã���ʹ��StateText������״̬
  - 0����ֹͣ
  - 1������ͣ�������ȴ���ʼ��
  - 2����������
  - 3����������
  - 4�����ڼ���Hash
  - 5������ֹͣ
  - 6������
  - 7�����ڻ�ȡԪ����
- StateText������״̬
  - WaitingForStart
  - Downloading
  - Paused
  - Seeding
  - Stopping
  - Stopped
  - Hashing
  - Metadata
  - Error
- TotalBytes�����������ܹ��ֽ���
- DownloadedBytes�������ص��ֽ���
- DownloadSpeed�������ٶȣ���λ�� Byte/s
- UploadSpeed���ϴ��ٶȣ���λ�� Byte/s
- RemainTime��ʣ��ʱ�䣬��λ���롣-1��ʾ�޷��������������ͣ
- SavePath�����ر���Ŀ¼
- Ignore�������أ������ԣ��ļ����б�ʹ�����·������ͬ�ļ�֮���á�|�����ŷָ���� 1.txt|example\2.txt|3.txt
- CreatedTime�����񴴽�ʱ�䣬ʹ��PCϵͳ�ĵ�ǰʱ��
- FirstFinishTime���״�������ɵ�ʱ�䣬����Ϊ`null`
- UpdatedTime��������Ϣ����ʱ�䣬����Ϊ`null`
- EnableAcceleration���û����������ʹ�á���Ա�������ء�
- EnteredAcceleration���������Ƿ��ѽ��롰��Ա�������ء�״̬
- IsDeleted���Ѿ�ɾ����������վ��
- LazyLoad�����û���������ʱ�ٳ�ʼ����ش��벢ˢ��������Ϣ
- Files�������а������ļ�
  - FileIndex���ļ���������`0`��ʼ
  - FileName���ļ�����
  - FilePath���ļ�����·��
  - Progress���ļ����ؽ��ȣ���Χ�� 0.0-1.0
  - FileSize���ļ��������λ�� Byte
- ContainingFolder�����������ļ��С������ǰ����Ϊ���ļ���BT������ֵΪ���ļ���·�������Ϊ���ļ���BT������ֵΪ������ĸ�Ŀ¼��

## 14.��ȡĳһ�����������Ϣ /api/v1/download/tasks/{taskId}

### ����

- taskId�����������ID����bt hash��Ϊ32λ���ȵĴ�д��ĸ�ַ���

### ����ֵ

��������ͬ�Ϸ�"��ȡ���������б�"API�ķ���ֵ��ֻ����һ��json����

```json
{
  "Id": "C7C1F5BEEC78122CCA8CBD0AEE8F8300C3192D3C",
  "Progress": 1,
  "IsDownloadFinished": true,
  "Title": "[DMG&MH][Shoujo Kageki Revue Starlight][09][720P][GB].mp4",
  "State": 6,
  "StateText": "Stopped",
  "TotalBytes": 128029807,
  "DownloadedBytes": 128029807,
  "DownloadSpeed": 0,
  "UploadSpeed": 0,
  "RemainTime": 0,
  "SavePath": "Y:\\��Ů���",
  "Ignore": "",
  "CreatedTime": "2018-09-23T18:04:50.4946945+08:00",
  "FirstFinishTime": null,
  "UpdatedTime": null,
  "EnableAcceleration": true,
  "EnteredAcceleration": false,
  "IsDeleted": false,
  "LazyLoad": true,
  "Files": [
    {
      "FileIndex": 0,
      "FileName": "[DMG&MH][Shoujo Kageki Revue Starlight][09][720P][GB].mp4",
      "FilePath": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][09][720P][GB].mp4",
      "Progress": 1,
      "FileSize": 128029807
    }
  ],
  "ContainingFolder": "Y:\\��Ů���\\[DMG&MH][Shoujo Kageki Revue Starlight][09][720P][GB].mp4"
}
```

## 15.����������� /api/v1/download/tasks/add?magnet={magnet}

### ����

- magnet����Ҫ������صĴ������ӣ��˲�����Ҫ�Ƚ���Url����Ȼ��ŵ������С��������ӱ��뺬�� `urn:btih=` ��

### ����ֵ

- ������񴴽��ɹ����򷵻ش��½��������Ϣ����ʽͬ"��ȡĳһ�����������Ϣ"API��ͬ��
- �������ID�Ѵ��ڣ�����ڸ��µ�ǰ��������֮�󷵻ش��������Ϣ��
- �����������ʧ�ܣ����᷵��`null`��

## 16.������������ /api/v1/download/tasks/{taskId}/{method}?remove={remove}

### ����

- taskId����������ID
- method����Ҫ���еĲ���
  - start����ʼ
  - pause����ͣ
  - delete��ɾ������
- remove��ɾ������ʱ�Ƿ�ɾ����Ӧ����Ƶ�ļ�
  - 1��ɾ���ļ�
  - 0����ɾ���������ļ�������`method`=`delete`ʱremove�����Ż���Ч��

### ����ֵ

���ش��������Ϣ�����ظ�ʽͬ "��ȡĳһ�����������Ϣ" API��ͬ��

## 17.ɨ��ý����ļ����е��ļ��Ķ� /api/v1/library/scan

ɨ��ý����������ļ����ļ��Ķ�+Ϊ����Ƶ��������ͼ+Ϊ����Ƶ������Ļ�⡣��������Ϸ��أ�ˢ�²������ں�̨���С�

## 18.����ý���������Ƶ�Ĺ�����Ϣ /api/v1/library/refreshmatch

��������ˢ��ý�����������Ƶ�Ĺ�����Ϣ����������Ϸ��أ�ˢ�²������ں�̨���С�