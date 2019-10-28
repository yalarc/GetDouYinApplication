文章链接：https://mp.weixin.qq.com/s?__biz=MzI4OTQxNjU2Mw==&mid=2247483973&idx=1&sn=e5f1fc8141993bedab4968cff9ac50d2&chksm=ec2e3659db59bf4f6dd2c8346980c96dacb99e01d518c233b20278c2f5de6b672e37d632bf88&token=829399530&lang=zh_CN#rd

导读：直接上干货，爬取抖音小姐姐视频列表，并去水印下载（仅供学习使用，不做商业用途，如有侵权，联系作者删除）；接18年初，Python基础篇更新。

比如我想获取抖音网红“惠子”小姐姐的主页列表视频，第一步在抖音上打开惠子的主页，右上角点击一下，可以看到一个分享按钮，点击分享，找到复制链接->  http://v.douyin.com/9GEGSp/ 。把链接放到浏览器中短链接被自动解析，变成长链接：
https://www.iesdouyin.com/share/user/73838190950?u_code=128dfi636&sec_uid=MS4wLjABAAAAHmQ4DqHKN8IdfWWd52sYaGS6zaZaOTghOZ4ysZ0z_YM&timestamp=1571884619&utm_source=copy&utm_campaign=client_share&utm_medium=android&share_app_name=douyin ，在长链接中就可以看到一些用户信息，有没有用我们先列出来！


key | value
---|---
user | 73838190950
u_code |128dfi636
sec_uid |MS4wLjABAAAAHmQ4DqHKN8IdfWWd52sYaGS6zaZaOTghOZ4ysZ0z_YM
timestamp |1571884619
utm_source |copy
utm_campaign |client_share
utm_medium |android
share_app_name |douyin

打开浏览器开发者工具，找到对应的视频列表请求接口，一个一个排查终于找到这个链接：https://www.iesdouyin.com/web/api/v2/aweme/post/?sec_uid=MS4wLjABAAAAHmQ4DqHKN8IdfWWd52sYaGS6zaZaOTghOZ4ysZ0z_YM&count=21&max_cursor=0&aid=1128&_signature=QOtJJBARHVwzHUNLqlT-mEDrST&dytk=593d265a74e3384e06112b423ef268da

key | value
---|---
sec_uid | MS4wLjABAAAAHmQ4DqHKN8IdfWWd52sYaGS6zaZaOTghOZ4ysZ0z_YM
count |21
max_cursor |1567769380000
aid |1128
_signature |F1OCixATSudkpYjkPsX5FRdTgp
dytk |593d265a74e3384e06112b423ef268da

返回的数据：

```
     Json:
{
"max_cursor": 1569668211000,
"min_cursor": 1571815003000,
"has_more": true,
-"extra": {
"now": 1571888892000,
"logid": "2019102411481201001404709304158BDD"
},
"status_code": 0,
-"aweme_list": [
-{
-"statistics": {
"aweme_id": "6750893105127378180",
"comment_count": 1240,
"digg_count": 30000,
"play_count": 675000,
"share_count": 79,
"forward_count": 17
},
"image_infos": null,
"uniqid_position": null,
"long_video": null,
"aweme_id": "6750893105127378180",
+"text_extra": [ … ],
"position": null,
"geofencing": null,
"promotions": null,
"desc": "#看啥啥都缺 ，爱买女孩绝不认输。",
"aweme_type": 4,
"comment_list": null,
"video_text": null,
"cha_list": null,
-"video": {
+"cover": { … },
"width": 720,
-"origin_cover": {
-"url_list": [
"http://p3-dy.byteimg.com/large/tos-cn-p-0015/6e83730009fe4fc2a3eeddbf06b0dbbf_1571815007.jpeg",
"http://p9-dy.byteimg.com/large/tos-cn-p-0015/6e83730009fe4fc2a3eeddbf06b0dbbf_1571815007.jpeg",
"http://p1-dy.byteimg.com/large/tos-cn-p-0015/6e83730009fe4fc2a3eeddbf06b0dbbf_1571815007.jpeg"
],
"uri": "large/tos-cn-p-0015/6e83730009fe4fc2a3eeddbf06b0dbbf_1571815007"
},
"has_watermark": false,
-"play_addr_lowbr": {
"uri": "v0200ff80000bmnvs5ignbh26fqqufbg",
-"url_list": [
"https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=0&ratio=540p&media_type=4&vr_type=0&improve_bitrate=0&is_play_url=1",
"https://api.amemv.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=1&ratio=540p&media_type=4&vr_type=0&improve_bitrate=0&is_play_url=1"
]
},
"bit_rate": null,
"vid": "v0200ff80000bmnvs5ignbh26fqqufbg",
-"play_addr": {
"uri": "v0200ff80000bmnvs5ignbh26fqqufbg",
-"url_list": [
"https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=0&ratio=540p&media_type=4&vr_type=0&improve_bitrate=0&is_play_url=1",
"https://api.amemv.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=1&ratio=540p&media_type=4&vr_type=0&improve_bitrate=0&is_play_url=1"
]
},
"height": 1280,
-"dynamic_cover": {
-"url_list": [
"https://p3-dy.byteimg.com/obj/tos-cn-p-0015/f4f71ff403574d768a87e7ef3501a7cc_1571815009",
"https://p9-dy.byteimg.com/obj/tos-cn-p-0015/f4f71ff403574d768a87e7ef3501a7cc_1571815009",
"https://p1-dy.byteimg.com/obj/tos-cn-p-0015/f4f71ff403574d768a87e7ef3501a7cc_1571815009"
],
"uri": "tos-cn-p-0015/f4f71ff403574d768a87e7ef3501a7cc_1571815009"
},
"ratio": "540p",
-"download_addr": {
"uri": "v0200ff80000bmnvs5ignbh26fqqufbg",
-"url_list": [
"https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=0&ratio=540p&watermark=0&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme_self",
"https://api.amemv.com/aweme/v1/play/?video_id=v0200ff80000bmnvs5ignbh26fqqufbg&line=1&ratio=540p&watermark=0&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme_self"
]
},
"duration": 61824
},
"video_labels": null,
"label_top_text": null
}
]
}
```
通过返回的参数可以看到我们需要的数据都在这里，在这里不着急解析数据，通过对比请求参数，别的参数都是现成的在主页代码中都可以找到，基本可以确定` _signature `参数是加密字符串，接下来我们就跟踪这个参数的形成过程。通过搜索，确定了它在`index_10ae3b3.js`中生成的 ，截图如下：

通过截图我们知道，`signature` 是通过`_bytedAcrawler`对象获取的，顺着我们查看它的生成过程：截图如下：

它是在`base_327cc85.js`生成的,截图如下：

通过分析，`_signature` 获取比较复杂，js代码已经被混淆压制，直接分析算法过程比较难，但是我们可以通过执行签名的算法代码，并返回对应的签名结果。把被压过的js保存下来，执行`_bytedAcrawler.sign("")`获取参数签名。

分析完成后，开始python模拟手机数据请求：

1.读取主页链接：支持同时爬去多个小姐姐的主页视频列表，在`share-url.txt`中输入每个URL通过逗号/空格/tab/表格鍵/回车符 分割，支持多行，也可以使用命令进行指定链接`python amemv-video-ripper.py url1,url2...`，解析文本数据/命令行数据；

```
 content, opts, args = None, None, []

    try:
        if len(sys.argv) >= 2:
            opts, args = getopt.getopt(sys.argv[1:], "hi:o:", ["favorite"])
    except getopt.GetoptError as err:
        usage()
        sys.exit(2)

    if not args:
        # check the sites file
        filename = "share-url.txt"
        if os.path.exists(filename):
            content = parse_sites(filename)
        else:
            usage()
            sys.exit(1)
    else:
        content = (args[0] if args else '').split(",")

    if len(content) == 0 or content[0] == "":
        usage()
        sys.exit(1)

    if opts:
        for o, val in opts:
            if o in ("--favorite"):
                download_favorite = True
                break

    CrawlerScheduler(content)
```
2.获取列表视频：

```
class CrawlerScheduler(object):

    def __init__(self, items):
        self.numbers = []
        self.challenges = []
        self.musics = []
        for i in range(len(items)):
            url = get_real_address(items[i])
            if not url:
                continue
            if re.search('share/user', url):
                self.numbers.append(url)
            if re.search('share/challenge', url):
                self.challenges.append(url)
            if re.search('share/music', url):
                self.musics.append(url)

        self.queue = Queue.Queue()
        self.scheduling()

    #通过node执行fuck-byted-acrawler.js得到签名
    @staticmethod
    def generateSignature(value):
        p = os.popen('node fuck-byted-acrawler.js %s' % value)
        return p.readlines()[0]

    @staticmethod
    def calculateFileMd5(filename):
        hmd5 = hashlib.md5()
        fp = open(filename, "rb")
        hmd5.update(fp.read())
        return hmd5.hexdigest()

    def scheduling(self):
        for x in range(THREADS):
            worker = DownloadWorker(self.queue)
            worker.daemon = True
            worker.start()

        for url in self.numbers:
            self.download_user_videos(url)
        for url in self.challenges:
            self.download_challenge_videos(url)
        for url in self.musics:
            self.download_music_videos(url)

    def download_user_videos(self, url):
        number = re.findall(r'share/user/(\d+)', url)
        if not len(number):
            return
        dytk = get_dytk(url)
        hostname = urllib.parse.urlparse(url).hostname
        if hostname != 't.tiktok.com' and not dytk:
            return
        user_id = number[0]
        video_count = self._download_user_media(user_id, dytk, url)
        self.queue.join()
        print("\nAweme number %s, video number %s\n\n" %
              (user_id, str(video_count)))
        print("\nFinish Downloading All the videos from %s\n\n" % user_id)

    def download_challenge_videos(self, url):
        challenge = re.findall('share/challenge/(\d+)', url)
        if not len(challenge):
            return
        challenges_id = challenge[0]
        video_count = self._download_challenge_media(challenges_id, url)
        self.queue.join()
        print("\nAweme challenge #%s, video number %d\n\n" %
              (challenges_id, video_count))
        print("\nFinish Downloading All the videos from #%s\n\n" % challenges_id)

    def download_music_videos(self, url):
        music = re.findall('share/music/(\d+)', url)
        if not len(music):
            return
        musics_id = music[0]
        video_count = self._download_music_media(musics_id, url)
        self.queue.join()
        print("\nAweme music @%s, video number %d\n\n" %
              (musics_id, video_count))
        print("\nFinish Downloading All the videos from @%s\n\n" % musics_id)

    def _join_download_queue(self, aweme, target_folder):
        try:
            if aweme.get('video', None):
                uri = aweme['video']['play_addr']['uri']
                download_url = "https://aweme.snssdk.com/aweme/v1/play/?{0}"
                download_params = {
                    'video_id': uri,
                    'line': '0',
                    'ratio': '720p',
                    'media_type': '4',
                    'vr_type': '0',
                    'test_cdn': 'None',
                    'improve_bitrate': '0',
                    'iid': '35628056608',
                    'device_id': '46166618999',
                    'os_api': '18',
                    'app_name': 'aweme',
                    'channel': 'App%20Store',
                    'idfa': '00000000-0000-0000-0000-000000000000',
                    'device_platform': 'iphone',
                    'build_number': '27014',
                    'vid': '2ED380A7-F09C-6C9E-90F5-862D58F3129C',
                    'openudid': '21dae85eeac1da35a69e2a0ffeaeef61c78a2e98',
                    'device_type': 'iPhone8%2C2',
                    'app_version': '2.7.0',
                    'version_code': '2.7.0',
                    'os_version': '12.0',
                    'screen_width': '1242',
                    'aid': '1128',
                    'ac': 'WIFI'
                }
                if aweme.get('hostname') == 't.tiktok.com':
                    download_url = 'http://api.tiktokv.com/aweme/v1/play/?{0}'
                    download_params = {
                        'video_id': uri,
                        'line': '0',
                        'ratio': '720p',
                        'media_type': '4',
                        'vr_type': '0',
                        'test_cdn': 'None',
                        'improve_bitrate': '0',
                        'version_code': '1.7.2',
                        'language': 'en',
                        'app_name': 'trill',
                        'vid': 'D7B3981F-DD46-45A1-A97E-428B90096C3E',
                        'app_version': '1.7.2',
                        'device_id': '6619780206485964289',
                        'channel': 'App Store',
                        'mcc_mnc': '',
                        'tz_offset': '28800'
                    }
                share_info = aweme.get('share_info', {})
                url = download_url.format(
                    '&'.join([key + '=' + download_params[key] for key in download_params]))
                self.queue.put(('video',
                                uri + "-" + share_info.get('share_desc', uri),
                                url, target_folder))
            else:
                if aweme.get('image_infos', None):
                    image = aweme['image_infos']['label_large']
                    self.queue.put(
                        ('image', image['uri'], image['url_list'][0], target_folder))

        except KeyError:
            return
        except UnicodeDecodeError:
            print("Cannot decode response data from DESC %s" % aweme['desc'])
            return


    def _download_user_media(self, user_id, dytk, url):
        current_folder = os.getcwd()
        target_folder = os.path.join(current_folder, 'download/%s' % user_id)
        if not os.path.isdir(target_folder):
            os.mkdir(target_folder)

        if not user_id:
            print("Number %s does not exist" % user_id)
            return
        hostname = urllib.parse.urlparse(url).hostname
        signature = self.generateSignature(str(user_id))
        user_video_url = "https://%s/aweme/v1/aweme/post/" % hostname
        user_video_params = {
            'user_id': str(user_id),
            'count': '21',
            'max_cursor': '0',
            'aid': '1128',
            '_signature': signature,
            'dytk': dytk
        }
        if hostname == 't.tiktok.com':
            user_video_params.pop('dytk')
            user_video_params['aid'] = '1180'

        max_cursor, video_count = None, 0
        while True:
            if max_cursor:
                user_video_params['max_cursor'] = str(max_cursor)
            res = requests.get(user_video_url, headers=HEADERS,
                               params=user_video_params)
            contentJson = json.loads(res.content.decode('utf-8'))
            aweme_list = contentJson.get('aweme_list', [])
            for aweme in aweme_list:
                video_count += 1
                aweme['hostname'] = hostname
                self._join_download_queue(aweme, target_folder)
            if contentJson.get('has_more'):
                max_cursor = contentJson.get('max_cursor')
            else:
                break
        # if True:
        #     favorite_folder = target_folder + '/favorite'
        #     video_count = self.__download_favorite_media(
        #         user_id, dytk, hostname, signature, favorite_folder, video_count)

        if video_count == 0:
            print("There's no video in number %s." % user_id)

        return video_count

    def _download_challenge_media(self, challenge_id, url):
        if not challenge_id:
            print("Challenge #%s does not exist" % challenge_id)
            return
        current_folder = os.getcwd()
        target_folder = os.path.join(
            current_folder, 'download/#%s' % challenge_id)
        if not os.path.isdir(target_folder):
            os.mkdir(target_folder)

        hostname = urllib.parse.urlparse(url).hostname
        signature = self.generateSignature(str(challenge_id) + '9' + '0')

        challenge_video_url = "https://%s/aweme/v1/challenge/aweme/" % hostname
        challenge_video_params = {
            'ch_id': str(challenge_id),
            'count': '9',
            'cursor': '0',
            'aid': '1128',
            'screen_limit': '3',
            'download_click_limit': '0',
            '_signature': signature
        }

        cursor, video_count = None, 0
        while True:
            if cursor:
                challenge_video_params['cursor'] = str(cursor)
                challenge_video_params['_signature'] = self.generateSignature(
                    str(challenge_id) + '9' + str(cursor))
            res = requests.get(challenge_video_url,
                               headers=HEADERS, params=challenge_video_params)
            try:
                contentJson = json.loads(res.content.decode('utf-8'))
            except:
                print(res.content)
            aweme_list = contentJson.get('aweme_list', [])
            if not aweme_list:
                break
            for aweme in aweme_list:
                aweme['hostname'] = hostname
                video_count += 1
                self._join_download_queue(aweme, target_folder)
                print("number: ", video_count)
            if contentJson.get('has_more'):
                cursor = contentJson.get('cursor')
            else:
                break
        if video_count == 0:
            print("There's no video in challenge %s." % challenge_id)
        return video_count

    def _download_music_media(self, music_id, url):
        if not music_id:
            print("Challenge #%s does not exist" % music_id)
            return
        current_folder = os.getcwd()
        target_folder = os.path.join(current_folder, 'download/@%s' % music_id)
        if not os.path.isdir(target_folder):
            os.mkdir(target_folder)

        hostname = urllib.parse.urlparse(url).hostname
        signature = self.generateSignature(str(music_id))
        music_video_url = "https://%s/aweme/v1/music/aweme/?{0}" % hostname
        music_video_params = {
            'music_id': str(music_id),
            'count': '9',
            'cursor': '0',
            'aid': '1128',
            'screen_limit': '3',
            'download_click_limit': '0',
            '_signature': signature
        }
        if hostname == 't.tiktok.com':
            for key in ['screen_limit', 'download_click_limit', '_signature']:
                music_video_params.pop(key)
            music_video_params['aid'] = '1180'

        cursor, video_count = None, 0
        while True:
            if cursor:
                music_video_params['cursor'] = str(cursor)
                music_video_params['_signature'] = self.generateSignature(
                    str(music_id) + '9' + str(cursor))

            url = music_video_url.format(
                '&'.join([key + '=' + music_video_params[key] for key in music_video_params]))
            res = requests.get(url, headers=HEADERS)
            contentJson = json.loads(res.content.decode('utf-8'))
            aweme_list = contentJson.get('aweme_list', [])
            if not aweme_list:
                break
            for aweme in aweme_list:
                aweme['hostname'] = hostname
                video_count += 1
                self._join_download_queue(aweme, target_folder)
            if contentJson.get('has_more'):
                cursor = contentJson.get('cursor')
            else:
                break
        if video_count == 0:
            print("There's no video in music %s." % music_id)
        return video_count
```
3.下载视频：

```
#下载相关的逻辑
def download(medium_type, uri, medium_url, target_folder):

    headers = copy.copy(HEADERS)
    file_name = uri
    if medium_type == 'video':
        file_name += '.mp4'
        headers['user-agent'] = 'Aweme/27014 CFNetwork/974.2.1 Darwin/18.0.0'
    elif medium_type == 'image':
        file_name += '.jpg'
        file_name = file_name.replace("/", "-")
    else:
        return

    file_path = os.path.join(target_folder, file_name)
    if os.path.isfile(file_path):
        print(file_name + " 已经爬取过了，文件保存在 " + file_path + " 放弃爬取")
        return

    print("Downloading %s from %s.\n" % (file_name, medium_url))
    # VIDEOID_DICT[VIDEO_ID] = 1  # 记录已经下载的视频
    retry_times = 0
    while retry_times < RETRY:
        try:
            resp = requests.get(medium_url, headers=headers, stream=True, timeout=TIMEOUT)
            if resp.status_code == 403:
                retry_times = RETRY
                print("Access Denied when retrieve %s.\n" % medium_url)
                raise Exception("Access Denied")
            with open(file_path, 'wb') as fh:
                for chunk in resp.iter_content(chunk_size=1024):
                    fh.write(chunk)
            break
        except:
            pass
        retry_times += 1
    else:
        try:
            os.remove(file_path)
        except OSError:
            pass
        print("Failed to retrieve %s from %s.\n" % (uri, medium_url))
        time.sleep(1)

```
4.其他：

```
#通过短链接-获取长链接
def get_real_address(url):
    if url.find('v.douyin.com') < 0:
        return url
    res = requests.get(url, headers=HEADERS, allow_redirects=False)
    return res.headers['Location'] if res.status_code == 302 else None

# 得到dytk参数
def get_dytk(url):
    res = requests.get(url, headers=HEADERS)
    if not res:
        return None
    dytk = re.findall("dytk: '(.*)'", res.content.decode('utf-8'))
    if len(dytk):
        return dytk[0]
    return None

# 下载管理器
class DownloadWorker(Thread):
    def __init__(self, queue):
        Thread.__init__(self)
        self.queue = queue

    def run(self):
        while True:
            medium_type, uri, download_url, target_folder = self.queue.get()
            download(medium_type, uri, download_url, target_folder)
            self.queue.task_done()
```

5.执行截图：



6.源码获取：


7.去水印说明：其实抖音列表返回了无水印视频链接和有水印链接，没有涉及对视频水印的处理

8.其他如果在执行中遇到问题可以加我WX交流 ： qhb0123(备注github)




























