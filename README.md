## How to watch tplink tapo camera on windows / mac ?

#### if you are on windows

download exe from https://github.com/msys2/msys2-installer/releases
(click Assets and download something like 'msys2-x86_64-20250221.exe')

install it and run msys2

copy followings and paste (right click then paste) and press enter and wait
```
echo -e '\nrtsp://USERNAME:PASSWORD@IP:554/stream1\n'
while read -r c; do
	for i in $(seq 1 254); do
		telnet $c.$i 554 2>&1 | grep -oE 'Connected to.*$' &
	done
done < <(netstat -r | awk '{print $4}' | grep -oE '[0-9]+\.[0-9]+\.[0-9]+' | sort -u | grep -v '127.0.0') | grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+'
```

with the found ip address press `ctrl + n` on VLC then type something like `rtsp://USERNAME:PASSWORD@IP:554/stream1` and press enter

https://www.youtube.com/watch?v=ymJwaGGB4I0

#### if you are on mac

open terminal then copy followings and paste (right click then paste) and press enter and wait
```
echo -e '\nrtsp://USERNAME:PASSWORD@IP:554/stream1\n'
while read -r c; do
	for i in $(seq 1 254); do
		nc -z $c.$i 554 2>&1 | grep -oE 'open$' &
	done
done < <(netstat -r | awk '{print $4}' | grep -oE '[0-9]+\.[0-9]+\.[0-9]+' | sort -u | grep -v '127.0.0') | grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+'
```

with the found ip address press `ctrl + n` on VLC then type something like `rtsp://USERNAME:PASSWORD@IP:554/stream1` and press enter

https://www.youtube.com/watch?v=ymJwaGGB4I0

---

[![demo](http://img.youtube.com/vi/ymJwaGGB4I0/0.jpg)](http://www.youtube.com/watch?v=ymJwaGGB4I0 "demo")
