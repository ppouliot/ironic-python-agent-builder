BUILD_DIR=UPLOAD
KERNEL=$(BUILD_DIR)/flatcar_production_pxe.vmlinuz
INITRD=$(BUILD_DIR)/flatcar_production_pxe_image-oem.cpio.gz

default: docker flatcar

docker: 
	./docker_build.bash

flatcar:
	mkdir -p $(BUILD_DIR)
	./flatcar-oem-inject.py oem $(BUILD_DIR)

clean:
	rm -rf ironic-python-agent
	rm -f oem/container.tar.gz
	rm -f $(INITRD)
	rm -f $(KERNEL)
	rm -rf ../.image_cache

docker_clean:
	./docker_clean.bash

iso: docker flatcar
	./iso-image-create -o $(BUILD_DIR)/ipa-flatcar.iso -i $(INITRD) -k $(KERNEL)

pin_latest:
	./pin_latest_flatcar.sh
