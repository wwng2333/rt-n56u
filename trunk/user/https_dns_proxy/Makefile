SRC_NAME = https_dns_proxy-master
THISDIR = $(shell pwd)

all: extract_test config_test 
	$(MAKE) -C $(SRC_NAME)

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		unzip $(SRC_NAME).zip ; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
        mkdir -p $(SRC_NAME)/build
        cd $(SRC_NAME)/build
        cmake -DCMAKE_TOOLCHAIN_FILE=../cross-mipsel-linux.cmake $(SRC_NAME)
        make

clean:
        rm -rf $(SRC_NAME)/build
        rm -f config_done

romfs:
        $(ROMFSINST) -p +x $(SRC_NAME)/build/https_dns_proxy /usr/bin/https_dns_proxy
