%.bin: %.asm
	nasm -f bin $< -o $@

master.img: boot.bin loader.bin
	yes | bximage -hd -mode="flat" -size=60 -q master.img
	dd if=boot.bin of=master.img bs=512 count=1 conv=notrunc
	dd if=loader.bin of=master.img bs=512 count=4 seek=2 conv=notrunc

.PHONY: clean
clean:
	rm -rf *.bin
	rm -rf *.img

.PHONY: bochs
bochs: master.img
	bochs -q
