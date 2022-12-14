# SPDX-License-Identifier: GPL-2.0

SAMSUMG_DTB := arch/$(SRCARCH)/boot/dts/samsung
QCOM_DTB := ../vendor/qcom

define __sec_dtbo_build
dtbo-$(2) += $(1)
$(1)-base := $(3)
endef

define sec_dtbo_build
$(foreach dtbo, $(1), $(eval $(call __sec_dtbo_build, $(dtbo),$(2),$(3))))
endef

# KONA BASE DTB
SEC_KONA_BASE_DTB := $(QCOM_DTB)/kona.dtb $(QCOM_DTB)/kona-v2.dtb $(QCOM_DTB)/kona-v2.1.dtb

ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)

SEC_KONA_SPU_DTBO := \
		common/kona-sec-system-update-overlay.dtbo

$(eval $(call sec_dtbo_build, \
		$(SEC_KONA_SPU_DTBO),$(CONFIG_ARCH_KONA),$(SEC_KONA_BASE_DTB)))

endif

ifeq ($(filter y,$(CONFIG_SEC_C2Q_PROJECT)),y)
dts-dirs += c2q
else ifeq ($(filter y,$(CONFIG_SEC_C1Q_PROJECT)),y)
dts-dirs += c1q
else ifeq ($(filter y,$(CONFIG_SEC_Z3Q_PROJECT)),y)
dts-dirs += z3q
else ifeq ($(filter y,$(CONFIG_SEC_Y2Q_PROJECT)),y)
dts-dirs += y2q
else ifeq ($(filter y,$(CONFIG_SEC_X1Q_PROJECT)),y)
dts-dirs += x1q
else ifeq ($(filter y,$(CONFIG_SEC_R8Q_PROJECT)),y)
dts-dirs += r8q
endif

always          := $(dtb-y)
subdir-y        := $(dts-dirs)

clean-files := *.dtb *.reverse.dts *.dtbo
