# lird-musicimport 'package:flutter/material.dart';

void main() {
  runApp(const KurdMusicApp());
}

class KurdMusicApp extends StatelessWidget {
  const KurdMusicApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Kurd Music',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        brightness: Brightness.dark,
        scaffoldBackgroundColor: const Color(0xFF121212),
        primaryColor: Colors.amber,
        colorScheme: const ColorScheme.dark(
          primary: Colors.amber,
          secondary: Colors.deepOrange,
        ),
      ),
      home: const MainScreen(),
    );
  }
}

class MainScreen extends StatefulWidget {
  const MainScreen({super.key});

  @override
  State<MainScreen> createState() => _MainScreenState();
}

class _MainScreenState extends State<MainScreen> {
  int _currentIndex = 0;

  final List<Widget> _screens = [
    const HomeScreen(),
    const SearchScreen(),
    const DownloadsScreen(),
    const SettingsScreen(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _screens[_currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        backgroundColor: const Color(0xFF1E1E1E),
        selectedItemColor: Colors.amber,
        unselectedItemColor: Colors.grey,
        type: BottomNavigationBarType.fixed,
        onTap: (index) {
          setState(() {
            _currentIndex = index;
          });
        },
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'سەرەتا'),
          BottomNavigationBarItem(icon: Icon(Icons.search), label: 'گەڕان'),
          BottomNavigationBarItem(icon: Icon(Icons.download), label: 'دابەزێنراوەکان'),
          BottomNavigationBarItem(icon: Icon(Icons.settings), label: 'رێکخستن'),
        ],
      ),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Kurd Music 🎵', style: TextStyle(fontWeight: FontWeight.bold)),
        backgroundColor: Colors.transparent,
        elevation: 0,
        actions: [
          IconButton(
            icon: const Icon(Icons.workspace_premium, color: Colors.amber),
            onPressed: () {
              // لێرەدا پەنجەرەی کڕینی پریمێم بە 10 هەزار دینار دەکرێتەوە
              showDialog(
                context: context,
                builder: (context) => AlertDialog(
                  title: const Text('ئاشتراکی ساڵانەی پریمێم'),
                  content: const Text('هەموو ڕیکلامەکان لابەرە و کوالێتی بەرز بەدەستبهێنە تەنها بە 10,000 دینار بۆ ساڵێک!'),
                  actions: [
                    TextButton(
                      onPressed: () => Navigator.pop(context),
                      child: const Text('پاشگەزبوونەوە'),
                    ),
                    ElevatedButton(
                      style: ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                      onPressed: () {
                        // لێرەدا سیستەمی پارەدانی گوگل پلێ / ئاپ ستۆر دەبەسترێتەوە
                        Navigator.pop(context);
                      },
                      child: const Text('کڕین ئێستا', style: TextStyle(color: Colors.black)),
                    ),
                  ],
                ),
              );
            },
          ),
        ],
      ),
      body: ListView(
        padding: const EdgeInsets.all(16.0),
        children: [
          const Text('نوێترین گۆرانییەکان', style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
          const SizedBox(height: 12),
          // نموونەی لیستی گۆرانییەکان
          _buildSongCard('گۆرانی یەکەم', 'هونەرمەند ١', '٥:٣٠'),
          _buildSongCard('گۆرانی دووەم', 'هونەرمەند ٢', '٣:٤٥'),
          _buildSongCard('گۆرانی سێیەم', 'هونەرمەند ٣', '٤:١٥'),
        ],
      ),
    );
  }

  Widget _buildSongCard(String title, String artist, String duration) {
    return Card(
      color: const Color(0xFF1E1E1E),
      margin: const EdgeInsets.only(bottom: 12),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
      child: ListTile(
        leading: Container(
          width: 50,
          height: 50,
          decoration: BoxDecoration(
            color: Colors.amber.withOpacity(0.2),
            borderRadius: BorderRadius.circular(8),
          ),
          child: const Icon(Icons.music_note, color: Colors.amber),
        ),
        title: Text(title, style: const TextStyle(fontWeight: FontWeight.bold)),
        subtitle: Text(artist, style: const TextStyle(color: Colors.grey)),
        trailing: Row(
          mainAxisSize: MainAxisSize.min,
          children: [
            Text(duration, style: const TextStyle(color: Colors.grey, fontSize: 12)),
            const SizedBox(width: 8),
            const Icon(Icons.download_rounded, color: Colors.amber),
          ],
        ),
      ),
    );
  }
}

class SearchScreen extends StatelessWidget {
  const SearchScreen({super.key});
  @override
  Widget build(BuildContext context) {
    return const Center(child: Text('لاپەڕەی گەڕان بە دوای گۆرانی و موزیکدا'));
  }
}

class DownloadsScreen extends StatelessWidget {
  const DownloadsScreen({super.key});
  @override
  Widget build(BuildContext context) {
    return const Center(child: Text('گۆرانییە داگیراوەکان بۆ گوێگرتنی بێ ئینتەرنێت (Offline)'));
  }
}

class SettingsScreen extends StatelessWidget {
  const SettingsScreen({super.key});
  @override
  Widget build(BuildContext context) {
    return const Center(child: Text('ڕێکخستنەکانی زمان (کوردی، ئینگلیزی، عەرەبی)'));
  }
}
