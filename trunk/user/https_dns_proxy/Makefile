SRC_NAME = https_dns_proxy-master
THISDIR = $(shell pwd)

all: extract_test config_test
	cmake $(SRC_NAME)
	$(MAKE) -C $(SRC_NAME)

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		unzip $(SRC_NAME).zip ; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		touch config_done; \
	fi )

configure:
	( mkdir -p $(SRC_NAME)/https_dns_proxy-master/build && cd $(SRC_NAME)/https_dns_proxy-master/build ; \
		cmake \
			-DCMAKE_TOOLCHAIN_FILE=../../cross-mipsel-linux.cmake \
			. ; \
	)

clean:
	rm -rf $(SRC_NAME)/https_dns_proxy-master/build
	rm -f config_done

romfs:
	$(ROMFSINST) -p +x $(SRC_NAME)/https_dns_proxy-master/build/https_dns_proxy /usr/bin/https_dns_proxy
