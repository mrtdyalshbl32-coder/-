import 'package:flutter/material.dart';

void main() {
  runApp(const AlSheblEmpireApp());
}

class AlSheblEmpireApp extends StatelessWidget {
  const AlSheblEmpireApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    const Color bloodRed = Color(0xFF8B0000);

    return MaterialApp(
      title: 'إمبراطورية آل شبل',
      debugShowCheckedModeBanner: false,
      theme: ThemeData.dark().copyWith(
        scaffoldBackgroundColor: const Color(0xFF090909),
        primaryColor: bloodRed,
        colorScheme: const ColorScheme.dark(
          primary: bloodRed,
          surface: Color(0xFF141414),
        ),
        appBarTheme: const AppBarTheme(
          backgroundColor: Color(0xFF090909),
          elevation: 0,
          centerTitle: true,
          titleTextStyle: TextStyle(color: bloodRed, fontSize: 18, fontWeight: FontWeight.bold),
          iconTheme: IconThemeData(color: bloodRed),
        ),
        bottomNavigationBarTheme: const BottomNavigationBarThemeData(
          backgroundColor: Color(0xFF101010),
          selectedItemColor: bloodRed,
          unselectedItemColor: Colors.grey,
          type: BottomNavigationBarType.fixed,
        ),
      ),
      home: const MainHomeScreen(),
    );
  }
}

class MainHomeScreen extends StatefulWidget {
  const MainHomeScreen({Key? key}) : super(key: key);

  @override
  State<MainHomeScreen> createState() => _MainHomeScreenState();
}

class _MainHomeScreenState extends State<MainHomeScreen> {
  int _currentIndex = 3;

  final List<Widget> _screens = [
    const FeedTab(),
    const ReelsTab(),
    const PollsTab(),
    const ChatListTab(),
    const UserProfileScreen(username: 'mortada_vip', displayName: '👑 ༺مرتضى آل شبل༻ 👑', isMe: true),
  ];

  @override
  Widget build(BuildContext context) {
    bool showStories = _currentIndex != 4;

    return Scaffold(
      appBar: AppBar(
        title: const Text('🏰 إمبراطورية مرتضى'),
        actions: [
          IconButton(
            icon: const Icon(Icons.search),
            onPressed: () => showSearch(context: context, delegate: UserSearchDelegate()),
          ),
        ],
      ),
      body: Column(
        children: [
          if (showStories) _buildStoriesBar(),
          Expanded(child: _screens[_currentIndex]),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        backgroundColor: const Color(0xFF8B0000),
        child: const Icon(Icons.add, color: Colors.white, size: 28),
        onPressed: () => _openCreateContentSheet(context),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) => setState(() => _currentIndex = index),
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.grid_view_rounded), label: 'البوستات'),
          BottomNavigationBarItem(icon: Icon(Icons.video_collection_rounded), label: 'الريلز'),
          BottomNavigationBarItem(icon: Icon(Icons.how_to_vote_rounded), label: 'التصويت'),
          BottomNavigationBarItem(icon: Icon(Icons.forum_rounded), label: 'الدردشات'),
          BottomNavigationBarItem(icon: Icon(Icons.person_rounded), label: 'حسابي'),
        ],
      ),
    );
  }

  Widget _buildStoriesBar() {
    final List<Map<String, String>> stories = [
      {'name': 'قصتك', 'isMe': 'true'},
      {'name': 'مرتضى', 'isMe': 'false'},
      {'name': 'علي', 'isMe': 'false'},
      {'name': 'حسين', 'isMe': 'false'},
      {'name': 'محمد', 'isMe': 'false'},
    ];

    return Container(
      height: 95,
      padding: const EdgeInsets.symmetric(vertical: 8),
      color: const Color(0xFF0D0D0D),
      child: ListView.builder(
        scrollDirection: Axis.horizontal,
        itemCount: stories.length,
        itemBuilder: (ctx, index) {
          final story = stories[index];
          return Padding(
            padding: const EdgeInsets.symmetric(horizontal: 8),
            child: GestureDetector(
              onTap: () {
                if (story['isMe'] == 'true') {
                  _pickMediaFromGallery(context, isVideo: false, title: 'نشر قصّة (Story) جديدة من المعرض');
                }
              },
              child: Column(
                children: [
                  Stack(
                    children: [
                      Container(
                        padding: const EdgeInsets.all(2.5),
                        decoration: BoxDecoration(
                          shape: BoxShape.circle,
                          gradient: story['isMe'] == 'true'
                              ? null
                              : const LinearGradient(colors: [Color(0xFF8B0000), Colors.amber]),
                        ),
                        child: const CircleAvatar(
                          radius: 26,
                          backgroundColor: Color(0xFF1F1F1F),
                          child: Icon(Icons.person, color: Colors.white),
                        ),
                      ),
                      if (story['isMe'] == 'true')
                        Positioned(
                          bottom: 0,
                          right: 0,
                          child: Container(
                            decoration: const BoxDecoration(color: Color(0xFF8B0000), shape: BoxShape.circle),
                            child: const Icon(Icons.add, size: 18, color: Colors.white),
                          ),
                        )
                    ],
                  ),
                  const SizedBox(height: 4),
                  Text(story['name']!, style: const TextStyle(fontSize: 11, color: Colors.grey)),
                ],
              ),
            ),
          );
        },
      ),
    );
  }

  void _openCreateContentSheet(BuildContext context) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF141414),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            const Text('إضافة محتوى جديد ✨', style: TextStyle(color: Colors.white, fontSize: 18, fontWeight: FontWeight.bold)),
            const SizedBox(height: 20),
            ListTile(
              leading: const Icon(Icons.article_rounded, color: Color(0xFF8B0000)),
              title: const Text('منشور جديد (Post) من المعرض', style: TextStyle(color: Colors.white)),
              onTap: () {
                Navigator.pop(ctx);
                _pickMediaFromGallery(context, isVideo: false, title: 'اختر صورة المنشور من المعرض');
              },
            ),
            ListTile(
              leading: const Icon(Icons.video_call_rounded, color: Colors.amber),
              title: const Text('فيديو ريلز جديد (Reels) من المعرض', style: TextStyle(color: Colors.white)),
              onTap: () {
                Navigator.pop(ctx);
                _pickMediaFromGallery(context, isVideo: true, title: 'اختر فيديو الريلز من المعرض');
              },
            ),
            ListTile(
              leading: const Icon(Icons.poll_rounded, color: Colors.blue),
              title: const Text('استطلاع رأي / تصويت (Poll)', style: TextStyle(color: Colors.white)),
              onTap: () { Navigator.pop(ctx); },
            ),
          ],
        ),
      ),
    );
  }

  void _pickMediaFromGallery(BuildContext context, {required bool isVideo, required String title}) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF1A1A1A),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => Container(
        height: 320,
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text(title, style: const TextStyle(color: Colors.white, fontSize: 15, fontWeight: FontWeight.bold)),
                IconButton(icon: const Icon(Icons.close, color: Colors.grey), onPressed: () => Navigator.pop(ctx)),
              ],
            ),
            const Divider(color: Colors.white10),
            const SizedBox(height: 10),
            Expanded(
              child: GridView.builder(
                gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                  crossAxisCount: 3,
                  crossAxisSpacing: 8,
                  mainAxisSpacing: 8,
                ),
                itemCount: 9,
                itemBuilder: (context, index) {
                  return InkWell(
                    onTap: () {
                      Navigator.pop(ctx);
                      ScaffoldMessenger.of(context).showSnackBar(
                        SnackBar(
                          content: Text('تم اختيار ${isVideo ? "الفيديو" : "الصورة"} رقم ${index + 1} بنجاح وقيد التحميل! 🚀'),
                          backgroundColor: const Color(0xFF8B0000),
                        ),
                      );
                    },
                    child: Container(
                      decoration: BoxDecoration(
                        color: const Color(0xFF2A2A2A),
                        borderRadius: BorderRadius.circular(8),
                        border: Border.all(color: Colors.white12),
                      ),
                      child: Stack(
                        alignment: Alignment.center,
                        children: [
                          Icon(
                            isVideo ? Icons.movie_creation_outlined : Icons.photo_size_select_actual_outlined,
                            color: Colors.white38,
                            size: 32,
                          ),
                          Positioned(
                            bottom: 4,
                            right: 4,
                            child: CircleAvatar(
                              radius: 10,
                              backgroundColor: const Color(0xFF8B0000),
                              child: Text('${index + 1}', style: const TextStyle(fontSize: 10, color: Colors.white)),
                            ),
                          )
                        ],
                      ),
                    ),
                  );
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class ChatListTab extends StatelessWidget {
  const ChatListTab({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    const Color bloodRed = Color(0xFF8B0000);

    return DefaultTabController(
      length: 3,
      child: Container(
        decoration: BoxDecoration(
          color: const Color(0xFF080808),
          image: DecorationImage(
            image: const NetworkImage('https://www.transparenttextures.com/patterns/dark-mosaic.png'),
            colorFilter: ColorFilter.mode(Colors.black.withOpacity(0.85), BlendMode.darken),
            fit: BoxFit.cover,
          ),
        ),
        child: Column(
          children: [
            Container(
              color: const Color(0xFF101010),
              child: const TabBar(
                indicatorColor: bloodRed,
                labelColor: bloodRed,
                unselectedLabelColor: Colors.grey,
                tabs: [
                  Tab(text: 'الخاصة'),
                  Tab(text: 'المجموعات'),
                  Tab(text: 'العامة'),
                ],
              ),
            ),
            Expanded(
              child: TabBarView(
                children: [
                  _buildPrivateChats(context),
                  _buildGroupChats(context),
                  _buildPublicChats(context),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildPrivateChats(BuildContext context) {
    return ListView(
      padding: const EdgeInsets.all(10),
      children: [
        _buildChatItem(
          context,
          name: 'علي الشبل',
          subtitle: 'آخر رسالة: هلا بيك أخي...',
          isGroup: false,
          isAdmin: false,
          type: 'private',
        ),
      ],
    );
  }

  Widget _buildGroupChats(BuildContext context) {
    return ListView(
      padding: const EdgeInsets.all(10),
      children: [
        _buildChatItem(
          context,
          name: 'مجموعة النخبة VIP 💎',
          subtitle: 'الأدمن: مرتضى آل شبل',
          isGroup: true,
          isAdmin: true,
          type: 'group',
        ),
      ],
    );
  }

  Widget _buildPublicChats(BuildContext context) {
    final List<Map<String, String>> topPublicChats = [
      {'title': '🔥 العامة الكبرى', 'activity': '1.2k متفاعل'},
      {'title': '💬 سوالف الشباب', 'activity': '850 متفاعل'},
      {'title': '🎮 مجتمع الجيمرز', 'activity': '430 متفاعل'},
    ];

    return Column(
      children: [
        Container(
          height: 100,
          padding: const EdgeInsets.symmetric(vertical: 10, horizontal: 8),
          child: ListView.builder(
            scrollDirection: Axis.horizontal,
            itemCount: topPublicChats.length,
            itemBuilder: (ctx, i) {
              final chat = topPublicChats[i];
              return Container(
                width: 130,
                margin: const EdgeInsets.only(right: 8),
                padding: const EdgeInsets.all(8),
                decoration: BoxDecoration(
                  color: const Color(0xFF181818),
                  borderRadius: BorderRadius.circular(12),
                  border: Border.all(color: const Color(0xFF8B0000).withOpacity(0.5)),
                ),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(chat['title']!, style: const TextStyle(color: Colors.white, fontSize: 12, fontWeight: FontWeight.bold), overflow: TextOverflow.ellipsis),
                    const SizedBox(height: 6),
                    Text(chat['activity']!, style: const TextStyle(color: Colors.amber, fontSize: 10)),
                  ],
                ),
              );
            },
          ),
        ),
        const Divider(color: Colors.white10),
        Expanded(
          child: ListView(
            padding: const EdgeInsets.all(10),
            children: [
              _buildChatItem(
                context,
                name: 'الدردشة العامة للإمبراطورية 👑',
                subtitle: 'مفتوحة للجميع • انضم الآن',
                isGroup: true,
                isAdmin: false,
                type: 'public',
              ),
            ],
          ),
        ),
      ],
    );
  }

  Widget _buildChatItem(BuildContext context, {required String name, required String subtitle, required bool isGroup, required bool isAdmin, required String type}) {
    return Card(
      color: const Color(0xFF121212).withOpacity(0.9),
      margin: const EdgeInsets.symmetric(vertical: 4),
      child: ListTile(
        leading: CircleAvatar(
          backgroundColor: const Color(0xFF8B0000),
          child: Icon(isGroup ? Icons.groups : Icons.person, color: Colors.white),
        ),
        title: Text(name, style: const TextStyle(color: Colors.white, fontWeight: FontWeight.bold)),
        subtitle: Text(subtitle, style: const TextStyle(color: Colors.grey, fontSize: 12)),
        onTap: () {
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (ctx) => ConversationScreen(
                chatName: name,
                isGroup: isGroup,
                isAdmin: isAdmin,
                type: type,
              ),
            ),
          );
        },
      ),
    );
  }
}

class ConversationScreen extends StatefulWidget {
  final String chatName;
  final bool isGroup;
  final bool isAdmin;
  final String type;

  const ConversationScreen({
    Key? key,
    required this.chatName,
    required this.isGroup,
    required this.isAdmin,
    required this.type,
  }) : super(key: key);

  @override
  State<ConversationScreen> createState() => _ConversationScreenState();
}

class _ConversationScreenState extends State<ConversationScreen> {
  Color _bgColor = const Color(0xFF090909);
  Color _bubbleColor = const Color(0xFF8B0000);
  Color _textColor = Colors.white;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: _bgColor,
      appBar: AppBar(
        title: Text(widget.chatName, style: const TextStyle(fontSize: 16)),
        actions: [
          IconButton(
            icon: const Icon(Icons.call, color: Colors.greenAccent),
            onPressed: () => _startCall(context, isVideo: false),
            tooltip: 'اتصال صوتي',
          ),
          IconButton(
            icon: const Icon(Icons.videocam, color: Colors.blueAccent),
            onPressed: () => _startCall(context, isVideo: true),
            tooltip: 'اتصال فيديو',
          ),
          IconButton(
            icon: const Icon(Icons.ondemand_video, color: Colors.amber),
            onPressed: () => _openWatchPartyDialog(context),
            tooltip: 'مشاهدة فيديو جماعي 🍿',
          ),
          if (widget.isGroup && widget.isAdmin && widget.type == 'group')
            IconButton(
              icon: const Icon(Icons.person_add_alt_1),
              onPressed: () => _openAddMemberDialog(context),
            ),
          IconButton(
            icon: const Icon(Icons.palette_outlined),
            onPressed: () => _openThemeCustomizer(context),
            tooltip: 'تخصيص ثيم وألوان الدردشة',
          ),
          if (widget.isGroup && widget.isAdmin)
            IconButton(
              icon: const Icon(Icons.settings),
              onPressed: () => _openGroupSettings(context),
            ),
        ],
      ),
      body: Column(
        children: [
          Expanded(
            child: ListView(
              padding: const EdgeInsets.all(12),
              children: [
                _buildBubble('أهلاً بك في ${widget.chatName}! 👋', false),
              ],
            ),
          ),
          Container(
            color: const Color(0xFF101010),
            padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 6),
            child: Row(
              children: [
                IconButton(
                  icon: const Icon(Icons.add_photo_alternate, color: Color(0xFF8B0000)),
                  onPressed: () => _openMediaPicker(context),
                ),
                Expanded(
                  child: TextField(
                    style: TextStyle(color: _textColor),
                    decoration: const InputDecoration(
                      hintText: 'اكتب رسالة...',
                      border: InputBorder.none,
                      hintStyle: TextStyle(color: Colors.grey),
                    ),
                  ),
                ),
                IconButton(
                  icon: const Icon(Icons.send_rounded, color: Color(0xFF8B0000)),
                  onPressed: () {},
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildBubble(String text, bool isMe) {
    return Align(
      alignment: isMe ? Alignment.centerRight : Alignment.centerLeft,
      child: Container(
        margin: const EdgeInsets.symmetric(vertical: 4),
        padding: const EdgeInsets.all(12),
        decoration: BoxDecoration(color: _bubbleColor, borderRadius: BorderRadius.circular(12)),
        child: Text(text, style: TextStyle(color: _textColor)),
      ),
    );
  }

  void _openWatchPartyDialog(BuildContext context) {
    TextEditingController urlController = TextEditingController();

    showDialog(
      context: context,
      builder: (ctx) => AlertDialog(
        backgroundColor: const Color(0xFF141414),
        title: Row(
          children: const [
            Icon(Icons.ondemand_video, color: Colors.amber),
            SizedBox(width: 8),
            Text('سينما المشاهدة الجماعية 🍿', style: TextStyle(color: Colors.white, fontSize: 16)),
          ],
        ),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              'اختر فيديو من معرض هاتفك أو أدخل رابط الفيديو/الفيلم للمشاهدة الجماعية:',
              style: TextStyle(color: Colors.grey, fontSize: 12),
            ),
            const SizedBox(height: 15),
            ElevatedButton.icon(
              style: ElevatedButton.styleFrom(
                backgroundColor: const Color(0xFF222222),
                minimumSize: const Size(double.infinity, 45),
                side: const BorderSide(color: Colors.amber),
              ),
              icon: const Icon(Icons.video_library_rounded, color: Colors.amber),
              label: const Text('اختيار فيديو من المعرض المحلي 📱', style: TextStyle(color: Colors.white, fontSize: 12)),
              onPressed: () {
                Navigator.pop(ctx);
                _launchWatchPartyRoom(context, "فيديو محلي من المعرض (Local Device Video)");
              },
            ),
            const SizedBox(height: 12),
            const Center(child: Text('أو عبر رابط شبكي', style: TextStyle(color: Colors.grey, fontSize: 11))),
            const SizedBox(height: 8),
            TextField(
              controller: urlController,
              style: const TextStyle(color: Colors.white),
              decoration: InputDecoration(
                hintText: 'ضع رابط الفيديو هنا (https://...)',
                hintStyle: const TextStyle(color: Colors.grey, fontSize: 12),
                filled: true,
                fillColor: const Color(0xFF222222),
                border: OutlineInputBorder(borderRadius: BorderRadius.circular(10), borderSide: BorderSide.none),
                prefixIcon: const Icon(Icons.link, color: Colors.amber),
              ),
            ),
          ],
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(ctx),
            child: const Text('إلغاء', style: TextStyle(color: Colors.grey)),
          ),
          ElevatedButton.icon(
            style: ElevatedButton.styleFrom(backgroundColor: const Color(0xFF8B0000)),
            icon: const Icon(Icons.play_arrow_rounded, color: Colors.white),
            label: const Text('بدء العرض للجميع', style: TextStyle(color: Colors.white)),
            onPressed: () {
              Navigator.pop(ctx);
              _launchWatchPartyRoom(context, urlController.text);
            },
          ),
        ],
      ),
    );
  }

  void _launchWatchPartyRoom(BuildContext context, String videoUrl) {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (ctx) => Scaffold(
          backgroundColor: Colors.black,
          appBar: AppBar(
            backgroundColor: const Color(0xFF101010),
            title: Text('🍿 عرض جماعي: ${widget.chatName}', style: const TextStyle(fontSize: 14)),
            actions: [
              IconButton(
                icon: const Icon(Icons.mic, color: Colors.greenAccent),
                onPressed: () {},
                tooltip: 'الصوت شغال المايك مفعل',
              ),
            ],
          ),
          body: Column(
            children: [
              Container(
                height: 230,
                width: double.infinity,
                color: const Color(0xFF151515),
                child: Stack(
                  alignment: Alignment.center,
                  children: [
                    const Icon(Icons.movie_creation, size: 80, color: Colors.white12),
                    Column(
                      mainAxisAlignment: MainAxisAlignment.center,
                      children: [
                        const Icon(Icons.play_circle_fill, size: 60, color: Colors.amber),
                        const SizedBox(height: 10),
                        Text(
                          videoUrl.isEmpty ? 'جاري تشغيل الفيديو المباشر...' : 'جاري التشغيل والسينما مفعلة من:\n$videoUrl',
                          textAlign: TextAlign.center,
                          style: const TextStyle(color: Colors.white70, fontSize: 12),
                        ),
                      ],
                    ),
                    const Positioned(
                      top: 10,
                      right: 10,
                      child: Chip(
                        avatar: Icon(Icons.record_voice_over, color: Colors.greenAccent, size: 16),
                        label: Text('الاتصال الصوتي مفعل 🎙️', style: TextStyle(fontSize: 10, color: Colors.white)),
                        backgroundColor: Colors.black54,
                      ),
                    ),
                  ],
                ),
              ),
              Expanded(
                child: Container(
                  color: const Color(0xFF090909),
                  child: ListView(
                    padding: const EdgeInsets.all(12),
                    children: [
                      const Center(
                        child: Chip(
                          label: Text('بدأ العرض الجماعي! استمتعوا بالمشاهدة 🍿', style: TextStyle(fontSize: 11, color: Colors.amber)),
                          backgroundColor: Color(0xFF1F1F1F),
                        ),
                      ),
                      _buildBubble('شنو رأيكم بـ هذا الفيلم؟ 🔥', false),
                    ],
                  ),
                ),
              ),
              Container(
                color: const Color(0xFF101010),
                padding: const EdgeInsets.all(8),
                child: Row(
                  children: [
                    const Expanded(
                      child: TextField(
                        style: TextStyle(color: Colors.white),
                        decoration: InputDecoration(
                          hintText: 'تفاعل مع أصدقائك هنا...',
                          border: InputBorder.none,
                          hintStyle: TextStyle(color: Colors.grey, fontSize: 13),
                        ),
                      ),
                    ),
                    IconButton(
                      icon: const Icon(Icons.send_rounded, color: Color(0xFF8B0000)),
                      onPressed: () {},
                    ),
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }

  void _startCall(BuildContext context, {required bool isVideo}) {
    showDialog(
      context: context,
      builder: (ctx) => AlertDialog(
        backgroundColor: const Color(0xFF141414),
        title: Row(
          children: [
            Icon(isVideo ? Icons.videocam : Icons.call, color: isVideo ? Colors.blueAccent : Colors.greenAccent),
            const SizedBox(width: 10),
            Text(isVideo ? 'اتصال فيديو' : 'اتصال صوتي', style: const TextStyle(color: Colors.white, fontSize: 16)),
          ],
        ),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            const CircleAvatar(
              radius: 40,
              backgroundColor: Color(0xFF8B0000),
              child: Icon(Icons.person, size: 45, color: Colors.white),
            ),
            const SizedBox(height: 15),
            Text('جاري الاتصال بـ ${widget.chatName}...', style: const TextStyle(color: Colors.grey, fontSize: 13)),
          ],
        ),
        actions: [
          Center(
            child: ElevatedButton.icon(
              style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
              icon: const Icon(Icons.call_end, color: Colors.white),
              label: const Text('إنهاء المكالمة', style: TextStyle(color: Colors.white)),
              onPressed: () => Navigator.pop(ctx),
            ),
          )
        ],
      ),
    );
  }

  void _openMediaPicker(BuildContext context) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF141414),
      builder: (ctx) => Padding(
        padding: const EdgeInsets.all(20),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            IconButton(
              icon: const Icon(Icons.image, color: Colors.blue, size: 30),
              onPressed: () {
                Navigator.pop(ctx);
                _showGalleryPickerSheet(context, 'اختر صورة لإرسالها بالدردشة');
              },
            ),
            IconButton(
              icon: const Icon(Icons.videocam, color: Colors.red, size: 30),
              onPressed: () {
                Navigator.pop(ctx);
                _showGalleryPickerSheet(context, 'اختر فيديو لإرساله بالدردشة');
              },
            ),
            IconButton(icon: const Icon(Icons.emoji_emotions, color: Colors.amber, size: 30), onPressed: () => Navigator.pop(ctx)),
          ],
        ),
      ),
    );
  }

  void _showGalleryPickerSheet(BuildContext context, String title) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF1A1A1A),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => Container(
        height: 300,
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            Text(title, style: const TextStyle(color: Colors.white, fontSize: 14, fontWeight: FontWeight.bold)),
            const SizedBox(height: 12),
            Expanded(
              child: GridView.builder(
                gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 3, crossAxisSpacing: 8, mainAxisSpacing: 8),
                itemCount: 6,
                itemBuilder: (ctx, index) => InkWell(
                  onTap: () {
                    Navigator.pop(ctx);
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(content: Text('تم إرسال العنصر المحدد من المعرض! 📩'), backgroundColor: const Color(0xFF8B0000)),
                    );
                  },
                  child: Container(
                    decoration: BoxDecoration(color: const Color(0xFF2A2A2A), borderRadius: BorderRadius.circular(8)),
                    child: const Icon(Icons.perm_media, color: Colors.white54),
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void _openThemeCustomizer(BuildContext context) {
    double hueVal = 0.0;
    Color selectedColor = _bubbleColor;

    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF141414),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => StatefulBuilder(
        builder: (context, setModalState) {
          return Padding(
            padding: const EdgeInsets.all(20),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                const Text('تخصيص لون ثيم الدردشة 🎨', style: TextStyle(color: Colors.white, fontSize: 16, fontWeight: FontWeight.bold)),
                const SizedBox(height: 15),
                Container(
                  height: 45,
                  decoration: BoxDecoration(color: selectedColor, borderRadius: BorderRadius.circular(10)),
                  child: const Center(child: Text('معاينة لون فقاعة الرسائل', style: TextStyle(color: Colors.white, fontWeight: FontWeight.bold))),
                ),
                const SizedBox(height: 20),
                const Text('حرك الشريط للتحكم بدرجة اللون المطلوبة:', style: TextStyle(color: Colors.grey, fontSize: 12)),
                const SizedBox(height: 10),
                SpectrumHueSlider(
                  hue: hueVal,
                  onChanged: (newHue) {
                    setModalState(() {
                      hueVal = newHue;
                      selectedColor = HSVColor.fromAHSV(1.0, hueVal, 0.85, 0.75).toColor();
                    });
                  },
                ),
                const SizedBox(height: 20),
                ElevatedButton(
                  style: ElevatedButton.styleFrom(backgroundColor: selectedColor, minimumSize: const Size(double.infinity, 45)),
                  onPressed: () {
                    setState(() {
                      _bubbleColor = selectedColor;
                    });
                    Navigator.pop(ctx);
                  },
                  child: const Text('تطبيق اللون على الدردشة', style: TextStyle(color: Colors.white)),
                )
              ],
            ),
          );
        },
      ),
    );
  }

  void _openAddMemberDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (ctx) => AlertDialog(
        backgroundColor: const Color(0xFF141414),
        title: const Text('إضافة عضو 👤', style: TextStyle(color: Color(0xFF8B0000))),
        content: const TextField(decoration: InputDecoration(hintText: 'ادخل اليوزر نيم...'), style: TextStyle(color: Colors.white)),
        actions: [
          TextButton(onPressed: () => Navigator.pop(ctx), child: const Text('إلغاء')),
          ElevatedButton(onPressed: () => Navigator.pop(ctx), child: const Text('إضافة')),
        ],
      ),
    );
  }

  void _openGroupSettings(BuildContext context) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF141414),
      builder: (ctx) => ListView(
        shrinkWrap: true,
        children: [
          ListTile(
            leading: const Icon(Icons.image, color: Colors.white),
            title: const Text('تغيير صورة/لوجو القروب من المعرض', style: TextStyle(color: Colors.white)),
            onTap: () {
              Navigator.pop(ctx);
              _showGalleryPickerSheet(context, 'اختر لوجو أو صورة القروب الجديدة من المعرض');
            },
          ),
          const ListTile(leading: Icon(Icons.edit, color: Colors.white), title: Text('تغيير اسم القروب', style: TextStyle(color: Colors.white))),
        ],
      ),
    );
  }
}

class SpectrumHueSlider extends StatelessWidget {
  final double hue;
  final ValueChanged<double> onChanged;

  const SpectrumHueSlider({Key? key, required this.hue, required this.onChanged}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 25,
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(15),
        gradient: const LinearGradient(
          colors: [
            Color(0xFFFF0000),
            Color(0xFFFFFF00),
            Color(0xFF00FF00),
            Color(0xFF00FFFF),
            Color(0xFF0000FF),
            Color(0xFFFF00FF),
            Color(0xFFFF0000),
          ],
        ),
      ),
      child: SliderTheme(
        data: SliderThemeData(
          trackShape: const RectangularSliderTrackShape(),
          overlayShape: SliderComponentShape.noOverlay,
          thumbShape: const RoundSliderThumbShape(enabledThumbRadius: 12),
          thumbColor: Colors.white,
        ),
        child: Slider(
          value: hue,
          min: 0.0,
          max: 360.0,
          onChanged: onChanged,
        ),
      ),
    );
  }
}

class UserProfileScreen extends StatefulWidget {
  final String username;
  final String displayName;
  final bool isMe;

  const UserProfileScreen({Key? key, required this.username, required this.displayName, this.isMe = false}) : super(key: key);

  @override
  State<UserProfileScreen> createState() => _UserProfileScreenState();
}

class _UserProfileScreenState extends State<UserProfileScreen> {
  late String _displayName;
  late String _username;
  Color _themeColor = const Color(0xFF8B0000);
  
  // حفظ صور البروفايل والغلاف بالثبات
  IconData _avatarIcon = Icons.person;
  IconData _coverIcon = Icons.landscape;

  // 📊 العدادات الشاملة (المحتوى والمتابعين)
  int _postsCount = 42;
  int _reelsCount = 18;
  int _pollsCount = 9;
  int _followersCount = 1250;
  int _followingCount = 180;

  @override
  void initState() {
    super.initState();
    _displayName = widget.displayName;
    _username = widget.username;
  }

  @override
  Widget build(BuildContext context) {
    // 🎨 جعل الصفحة كاملة بلون موحد وجذاب من الأعلى للأسفل
    return Container(
      color: _themeColor.withOpacity(0.25),
      child: SingleChildScrollView(
        child: Column(
          children: [
            // غلاف الحساب والصورة الشخصية المحفوظة
            Stack(
              clipBehavior: Clip.none,
              alignment: Alignment.bottomCenter,
              children: [
                Container(
                  height: 140,
                  width: double.infinity,
                  decoration: BoxDecoration(
                    color: _themeColor,
                    boxShadow: [
                      BoxShadow(color: Colors.black.withOpacity(0.3), blurRadius: 10, offset: const Offset(0, 4)),
                    ],
                  ),
                  child: Center(
                    child: Icon(_coverIcon, color: Colors.white.withOpacity(0.6), size: 50),
                  ),
                ),
                Positioned(
                  bottom: -38,
                  child: Container(
                    padding: const EdgeInsets.all(4),
                    decoration: BoxDecoration(color: _themeColor, shape: BoxShape.circle),
                    child: CircleAvatar(
                      radius: 40,
                      backgroundColor: const Color(0xFF1B1B1B),
                      child: Icon(_avatarIcon, size: 45, color: Colors.white),
                    ),
                  ),
                ),
              ],
            ),
            const SizedBox(height: 48),
            Text(_displayName, style: const TextStyle(color: Colors.white, fontSize: 19, fontWeight: FontWeight.bold)),
            Text('@$_username', style: const TextStyle(color: Colors.white70, fontSize: 13)),
            
            if (widget.isMe) ...[
              const SizedBox(height: 14),
              ElevatedButton.icon(
                style: ElevatedButton.styleFrom(
                  backgroundColor: _themeColor,
                  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(20)),
                  padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 10),
                ),
                icon: const Icon(Icons.edit, color: Colors.white, size: 16),
                label: const Text('تعديل البروفايل والألوان', style: TextStyle(color: Colors.white, fontSize: 13, fontWeight: FontWeight.bold)),
                onPressed: () => _openEditProfileSheet(context),
              ),
            ],

            const SizedBox(height: 20),
            
            // 📊 عداد المحتوى المضاف (بوستات، ريلز، تصويت، متابعين، يتابع) جنبًا إلى جنب
            Container(
              margin: const EdgeInsets.symmetric(horizontal: 10),
              padding: const EdgeInsets.symmetric(vertical: 12, horizontal: 8),
              decoration: BoxDecoration(
                color: _themeColor.withOpacity(0.4),
                borderRadius: BorderRadius.circular(15),
                border: Border.all(color: Colors.white24),
              ),
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: [
                  _buildStatItem('بوست', '$_postsCount', Icons.grid_view_rounded),
                  _buildStatItem('ريلز', '$_reelsCount', Icons.video_collection_rounded),
                  _buildStatItem('تصويت', '$_pollsCount', Icons.how_to_vote_rounded),
                  _buildStatItem('متابِعون', '$_followersCount', Icons.people_rounded),
                  _buildStatItem('يتابع', '$_followingCount', Icons.person_add_alt_1_rounded),
                ],
              ),
            ),

            const SizedBox(height: 300), // مساحة التمرير بلون الصفحة الموحد
          ],
        ),
      ),
    );
  }

  // ✏️ نافذة تعديل البروفايل وحفظ الصور والتنسيق الموحد
  void _openEditProfileSheet(BuildContext context) {
    TextEditingController nameController = TextEditingController(text: _displayName);
    TextEditingController userController = TextEditingController(text: _username);
    double tempHue = 0.0;
    Color tempColor = _themeColor;
    
    IconData tempAvatar = _avatarIcon;
    IconData tempCover = _coverIcon;

    showModalBottomSheet(
      context: context,
      isScrollControlled: true,
      backgroundColor: const Color(0xFF141414),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => StatefulBuilder(
        builder: (context, setModalState) {
          return Padding(
            padding: EdgeInsets.only(
              bottom: MediaQuery.of(context).viewInsets.bottom + 20,
              top: 20,
              left: 20,
              right: 20,
            ),
            child: SingleChildScrollView(
              child: Column(
                mainAxisSize: MainAxisSize.min,
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  const Center(child: Text('تعديل الملف الشخصي وتثبيت الحفظ 👑', style: TextStyle(color: Colors.white, fontSize: 18, fontWeight: FontWeight.bold))),
                  const SizedBox(height: 20),
                  
                  TextField(
                    controller: nameController,
                    style: const TextStyle(color: Colors.white),
                    decoration: const InputDecoration(labelText: 'الاسم الظاهر', labelStyle: TextStyle(color: Colors.grey)),
                  ),
                  const SizedBox(height: 10),
                  TextField(
                    controller: userController,
                    style: const TextStyle(color: Colors.white),
                    decoration: const InputDecoration(labelText: 'اسم المستخدم (اليوزر)', labelStyle: TextStyle(color: Colors.grey)),
                  ),
                  const SizedBox(height: 20),

                  // 🖼️ اختيار وتغيير صورة البروفايل من المعرض
                  ElevatedButton.icon(
                    style: ElevatedButton.styleFrom(backgroundColor: const Color(0xFF222222), minimumSize: const Size(double.infinity, 40)),
                    icon: const Icon(Icons.photo_library, color: Colors.amber),
                    label: const Text('اختيار صورة البروفايل من المعرض 🖼️', style: TextStyle(color: Colors.white, fontSize: 12)),
                    onPressed: () {
                      _pickImageFromGallery(context, 'صورة البروفايل');
                    },
                  ),
                  const SizedBox(height: 8),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceAround,
                    children: [
                      IconButton(
                        icon: Icon(Icons.person, color: tempAvatar == Icons.person ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempAvatar = Icons.person),
                      ),
                      IconButton(
                        icon: Icon(Icons.workspace_premium, color: tempAvatar == Icons.workspace_premium ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempAvatar = Icons.workspace_premium),
                      ),
                      IconButton(
                        icon: Icon(Icons.military_tech, color: tempAvatar == Icons.military_tech ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempAvatar = Icons.military_tech),
                      ),
                    ],
                  ),
                  const SizedBox(height: 15),

                  // 🖼️ اختيار وتغيير صورة الغلاف من المعرض
                  ElevatedButton.icon(
                    style: ElevatedButton.styleFrom(backgroundColor: const Color(0xFF222222), minimumSize: const Size(double.infinity, 40)),
                    icon: const Icon(Icons.panorama, color: Colors.amber),
                    label: const Text('اختر صورة الغلاف من معرض هاتفك 🌄', style: TextStyle(color: Colors.white, fontSize: 12)),
                    onPressed: () {
                      _pickImageFromGallery(context, 'صورة الغلاف');
                    },
                  ),
                  const SizedBox(height: 8),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceAround,
                    children: [
                      IconButton(
                        icon: Icon(Icons.landscape, color: tempCover == Icons.landscape ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempCover = Icons.landscape),
                      ),
                      IconButton(
                        icon: Icon(Icons.castle, color: tempCover == Icons.castle ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempCover = Icons.castle),
                      ),
                      IconButton(
                        icon: Icon(Icons.auto_awesome, color: tempCover == Icons.auto_awesome ? tempColor : Colors.grey, size: 32),
                        onPressed: () => setModalState(() => tempCover = Icons.auto_awesome),
                      ),
                    ],
                  ),
                  const SizedBox(height: 15),

                  // 🎨 شريط توحيد لون الصفحة بالكامل
                  const Text('تغيير لون الصفحة بالكامل من الأعلى للأسفل:', style: TextStyle(color: Colors.grey, fontSize: 12)),
                  const SizedBox(height: 10),
                  Container(
                    height: 35,
                    width: double.infinity,
                    decoration: BoxDecoration(color: tempColor, borderRadius: BorderRadius.circular(8)),
                    child: const Center(child: Text('معاينة اللون الموحد', style: TextStyle(color: Colors.white, fontSize: 12, fontWeight: FontWeight.bold))),
                  ),
                  const SizedBox(height: 10),
                  SpectrumHueSlider(
                    hue: tempHue,
                    onChanged: (newHue) {
                      setModalState(() {
                        tempHue = newHue;
                        tempColor = HSVColor.fromAHSV(1.0, tempHue, 0.85, 0.75).toColor();
                      });
                    },
                  ),
                  const SizedBox(height: 25),

                  // 💾 زر التأكيد وتثبيت الحفظ
                  ElevatedButton.icon(
                    style: ElevatedButton.styleFrom(backgroundColor: tempColor, minimumSize: const Size(double.infinity, 45)),
                    icon: const Icon(Icons.check_circle, color: Colors.white),
                    label: const Text('حفظ التعديلات والتثبيت', style: TextStyle(color: Colors.white, fontWeight: FontWeight.bold)),
                    onPressed: () {
                      setState(() {
                        _displayName = nameController.text;
                        _username = userController.text;
                        _themeColor = tempColor;
                        _avatarIcon = tempAvatar;
                        _coverIcon = tempCover;
                      });
                      Navigator.pop(ctx);
                    },
                  ),
                ],
              ),
            ),
          );
        },
      ),
    );
  }

  void _pickImageFromGallery(BuildContext context, String targetText) {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF1A1A1A),
      shape: const RoundedRectangleBorder(borderRadius: BorderRadius.vertical(top: Radius.circular(20))),
      builder: (ctx) => Container(
        height: 280,
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            Text('اختر $targetText من معرض الصور', style: const TextStyle(color: Colors.white, fontSize: 14, fontWeight: FontWeight.bold)),
            const SizedBox(height: 15),
            Expanded(
              child: GridView.builder(
                gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 3, crossAxisSpacing: 8, mainAxisSpacing: 8),
                itemCount: 6,
                itemBuilder: (ctx, index) => InkWell(
                  onTap: () {
                    Navigator.pop(ctx);
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(content: Text('تم تعيين الصورة $index كـ $targetText جديدة! 🎨'), backgroundColor: const Color(0xFF8B0000)),
                    );
                  },
                  child: Container(
                    decoration: BoxDecoration(color: const Color(0xFF2A2A2A), borderRadius: BorderRadius.circular(8)),
                    child: const Icon(Icons.image, color: Colors.amber),
                  ),
                ),
              ),
            )
          ],
        ),
      ),
    );
  }

  Widget _buildStatItem(String label, String count, IconData icon) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        Icon(icon, color: Colors.white70, size: 16),
        const SizedBox(height: 4),
        Text(count, style: const TextStyle(color: Colors.white, fontSize: 14, fontWeight: FontWeight.bold)),
        const SizedBox(height: 2),
        Text(label, style: const TextStyle(color: Colors.white70, fontSize: 10)),
      ],
    );
  }
}

class FeedTab extends StatelessWidget { const FeedTab({Key? key}) : super(key: key); @override Widget build(BuildContext context) => const Center(child: Text('📲 قسم المنشورات', style: TextStyle(color: Colors.white))); }
class ReelsTab extends StatelessWidget { const ReelsTab({Key? key}) : super(key: key); @override Widget build(BuildContext context) => const Center(child: Text('🎬 قسم الريلز', style: TextStyle(color: Colors.white))); }
class PollsTab extends StatelessWidget { const PollsTab({Key? key}) : super(key: key); @override Widget build(BuildContext context) => const Center(child: Text('📊 قسم التصويت', style: TextStyle(color: Colors.white))); }

class UserSearchDelegate extends SearchDelegate {
  @override List<Widget>? buildActions(BuildContext context) => [IconButton(icon: const Icon(Icons.clear), onPressed: () => query = '')];
  @override Widget? buildLeading(BuildContext context) => IconButton(icon: const Icon(Icons.arrow_back), onPressed: () => close(context, null));
  @override Widget buildResults(BuildContext context) => Center(child: Text('بحث: $query'));
  @override Widget buildSuggestions(BuildContext context) => const Center(child: Text('ابحث بـ اليوزر نيم...', style: TextStyle(color: Colors.grey)));
}
