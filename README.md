[Dictionary scanner.txt](https://github.com/user-attachments/files/29745085/Dictionary.scanner.txt)[Uploading Dictipython
import datetime
from pathlib import Path

class FileItem:
    def init(self, path: Path):
        self.name = path.name
        self.extension = path.suffix if path.suffix else "No Extension"
        
        stat = path.stat()
        self.sizebytes = stat.stsize
        self.lastmodified = datetime.datetime.fromtimestamp(stat.stmtime)

    def formatsize(self) -> str:
        for unit in ['B', 'KB', 'MB', 'GB']:
            if self.sizebytes < 1024:
                return f"{self.sizebytes:.2f} {unit}"
            self.sizebytes /= 1024
        return f"{self.sizebytes:.2f} TB"

    def str(self) -> str:
        return (f"[FILE] {self.name}\n"
                f"  Ext: {self.extension}\n"
                f"  Size: {self.formatsize()}\n"
                f"  Modified: {self.lastmodified.strftime('%Y-%m-%d %H:%M:%S')}\n")

class DirectoryScanner:
    def init(self, targetdirectory: str):
        self.targetpath = Path(targetdirectory)
        self.subfolders = []
        self.files = []

    def scan(self):
        if not self.targetpath.exists() or not self.targetpath.isdir():
            raise FileNotFoundError(f"The directory '{self.targetpath}' does not exist.")

        for item in self.targetpath.iterdir():
            if item.isdir():
                self.subfolders.append(item.name)
            elif item.isfile():
                self.files.append(FileItem(item))

    def savereport(self, outputfilename: str = "scanreport.txt"):
        with open(outputfilename, "w", encoding="utf-8") as f:
            f.write(f"=== SCAN REPORT FOR: {self.targetpath.resolve()} ===\n\n")
            
            f.write(f"--- SUBFOLDERS ({len(self.subfolders)}) ---\n")
            for folder in sorted(self.subfolders):
                f.write(f"[DIR]  {folder}\n")
            
            f.write(f"\n--- FILES ({len(self.files)}) ---\n")
            for fileitem in sorted(self.files, key=lambda x: x.name):
                f.write(str(fileitem))
                
        print(f"Success: Report generated and saved to '{outputfilename}'")

if name == "main":
    scanner = DirectoryScanner(".")
    scanner.scan()
    scanner.savereport("scanreport.txt")

Success: Report generated and saved to 'scanreport.txt'

python
import datetime
from pathlib import Path

class FileItem:
    def init(self, path: Path):
        self.name = path.name
        self.extension = path.suffix if path.suffix else "No Extension"

        stat = path.stat()
        self.sizebytes = stat.stsize
        self.lastmodified = datetime.datetime.fromtimestamp(stat.stmtime)

    def formatsize(self) -> str:
        size = self.sizebytes  # Use a local variable so original size isn't changed

        for unit in ['B', 'KB', 'MB', 'GB']:
            if size < 1024:
                return f"{size:.2f} {unit}"
            size /= 1024

        return f"{size:.2f} TB"

    def str(self):
        return (
            f"[FILE] {self.name}\n"
            f"  Ext: {self.extension}\n"
            f"  Size: {self.formatsize()}\n"
            f"  Modified: {self.lastmodified.strftime('%Y-%m-%d %H:%M:%S')}\n"
        )

class DirectoryScanner:
    def init(self, targetdirectory: str):
        self.targetpath = Path(targetdirectory)
        self.subfolders = []
        self.files = []

    def scan(self):
        # Check if directory exists
        if not self.targetpath.exists() or not self.targetpath.isdir():
            raise FileNotFoundError(
                f"The directory '{self.targetpath}' does not exist."
            )

        # Scan directory
        for item in self.targetpath.iterdir():
            if item.isdir():
                self.subfolders.append(item.name)
            elif item.isfile():
                self.files.append(FileItem(item))

    def savereport(self, outputfilename="scanreport.txt"):
        with open(outputfilename, "w", encoding="utf-8") as f:

            f.write(f"=== SCAN REPORT FOR: {self.targetpath.resolve()} ===\n\n")

            f.write(f"--- SUBFOLDERS ({len(self.subfolders)}) ---\n")
            for folder in sorted(self.subfolders):
                f.write(f"[DIR] {folder}\n")

            f.write(f"\n--- FILES ({len(self.files)}) ---\n")

            for fileitem in sorted(self.files, key=lambda x: x.name):
                f.write(str(fileitem))

        print(f"Success: Report generated and saved to '{outputfilename}'")

if name == "main":
    scanner = DirectoryScanner(".")   # Scan current directory
    scanner.scan()
    scanner.savereport("scanreport.txt")

Success: Report generated and saved to 'scanreport.txt'

python
import datetime
from pathlib import Path

class FileItem:
    def init(self, path: Path):
        self.name = path.name
        self.extension = path.suffix if path.suffix else "No Extension"

        stat = path.stat()
        self.sizebytes = stat.stsize
        self.lastmodified = datetime.datetime.fromtimestamp(stat.stmtime)

    def formatsize(self):
        size = self.sizebytes

        for unit in ['B', 'KB', 'MB', 'GB']:
            if size < 1024:
                return f"{size:.2f} {unit}"
            size /= 1024

        return f"{size:.2f} TB"

    def str(self):
        return (
            f"[FILE] {self.name}\n"
            f"  Extension: {self.extension}\n"
            f"  Size: {self.formatsize()}\n"
            f"  Last Modified: {self.lastmodified.strftime('%Y-%m-%d %H:%M:%S')}\n"
        )

class DirectoryScanner:
    def init(self, targetdirectory):
        self.targetpath = Path(targetdirectory)
        self.subfolders = []
        self.files = []

    def scan(self):
        if not self.targetpath.exists():
            raise FileNotFoundError(f"Directory not found: {self.targetpath}")

        if not self.targetpath.isdir():
            raise NotADirectoryError(f"{self.targetpath} is not a directory")

        for item in self.targetpath.iterdir():
            if item.isdir():
                self.subfolders.append(item.name)
            elif item.isfile():
                self.files.append(FileItem(item))

    def savereport(self, outputfilename="scanreport.txt"):
        with open(outputfilename, "w", encoding="utf-8") as f:
            f.write(f"=== SCAN REPORT ===\n")
            f.write(f"Directory: {self.targetpath.resolve()}\n\n")

            f.write(f"SUBFOLDERS ({len(self.subfolders)})\n")
            f.write("-"  40 + "\n")
            for folder in sorted(self.subfolders):
                f.write(f"[DIR] {folder}\n")

            f.write(f"\nFILES ({len(self.files)})\n")
            f.write("-"  40 + "\n")
            for file in sorted(self.files, key=lambda x: x.name):
                f.write(str(file))
                f.write("\n")

        print(f"Success! Report saved as '{outputfilename}'.")

if name == "main":
    scanner = DirectoryScanner(r"C:\Users\Laptop Lab\Desktop\test file")
    scanner.scan()
    scanner.savereport("scanreport.txt")

Success! Report saved as 'scanreport.txt'.

python
import datetime
from pathlib import Path

class FileItem:
    def init(self, path: Path):
        self.name = path.name
        self.extension = path.suffix if path.suffix else "No Extension"

        stat = path.stat()
        self.sizebytes = stat.stsize
        self.lastmodified = datetime.datetime.fromtimestamp(stat.stmtime)

    def formatsize(self):
        size = self.sizebytes

        for unit in ['B', 'KB', 'MB', 'GB']:
            if size < 1024:
                return f"{size:.2f} {unit}"
            size /= 1024

        return f"{size:.2f} TB"

    def str(self):
        return (
            f"[FILE] {self.name}\n"
            f"  Extension: {self.extension}\n"
            f"  Size: {self.formatsize()}\n"
            f"  Last Modified: {self.lastmodified.strftime('%Y-%m-%d %H:%M:%S')}\n"
        )

class DirectoryScanner:
    def init(self, targetdirectory):
        self.targetpath = Path(targetdirectory)
        self.subfolders = []
        self.files = []

    def scan(self):
        if not self.targetpath.exists():
            raise FileNotFoundError(f"Directory not found: {self.targetpath}")

        if not self.targetpath.isdir():
            raise NotADirectoryError(f"{self.targetpath} is not a directory")

        for item in self.targetpath.iterdir():
            if item.isdir():
                self.subfolders.append(item.name)
            elif item.isfile():
                self.files.append(FileItem(item))

    def savereport(self, outputfilename="scanreport.txt"):
        with open(outputfilename, "w", encoding="utf-8") as f:
            f.write(f"=== SCAN REPORT ===\n")
            f.write(f"Directory: {self.targetpath.resolve()}\n\n")

            f.write(f"SUBFOLDERS ({len(self.subfolders)})\n")
            f.write("-"  40 + "\n")
            for folder in sorted(self.subfolders):
                f.write(f"[DIR] {folder}\n")

            f.write(f"\nFILES ({len(self.files)})\n")
            f.write("-"  40 + "\n")
            for file in sorted(self.files, key=lambda x: x.name):
                f.write(str(file))
                f.write("\n")

        print(f"Success! Report saved as '{outputfilename}'.")

if name == "main":
    scanner = DirectoryScanner(r"C:\Users\Laptop Lab\Desktop\test file")
    scanner.scan()
    scanner.savereport("scanreport.txt")

Success! Report saved as 'scanreport.txt'.onary scanner.txt…]()
# Dictionary-scanner
