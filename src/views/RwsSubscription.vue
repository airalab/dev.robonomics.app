<template>
  <robo-layout-section>
     <robo-section width="narrow" centered >
      <robo-grid class="flex-container" type="flex" offset="x05" gap="x025" galign="start">
        <robo-text :title="2" offset="x025" align="center">Connect your account that has available XRT</robo-text>
        <robo-text size="tiny" weight="bold">Choose your account:</robo-text>
        <robo-account-polkadot
          short 
          extensionAllowShift
          extensionShowIcon
          selectable
          selectstyle
          selectblock
          :selecttitle="store.state.robonomicsUIvue.polkadot.address ? 'Switch a network' : 'Connect an account / Switch a network'"
        />
      </robo-grid>

      <robo-account-polkadot-subscription
        v-if="store.state.robonomicsUIvue.polkadot.address"
        @update:selected="selected = $event"
        @accountAdded="onAccountAdded"
        @error="onError"
      />

      <robo-account-polkadot-transfer
        v-if="recipient"
        :currentAccount="account"
        :balance="balanceInXRT"
        :recipient="recipient"
        @transferSuccess="onTransferSuccess"
        @transferError="onTransferError"
      />

      <!-- Subscription Buy Section -->
      <robo-account-polkadot-subscription-buy
        v-if="isTransferSuccess"
        :accountPr="recipient"
        :balance="balance"
      />
    </robo-section>
  </robo-layout-section>
</template>

<script setup>
import { useAccount } from "@/hooks/useAccount";
import { useBalance } from "@/hooks/useBalance";
import { ref, computed, watch } from "vue";
import { fromWei } from "@/utils/tools";
import { useStore } from "vuex";

const store = useStore();

const { account } = useAccount();
const { balance } = useBalance(account);

const recipient = ref(null);
const isTransferSuccess = ref(false)

const balanceInXRT = computed(() => balance.value ? fromWei(balance.value, 9) : 0);

const onAccountAdded = (addedPair) => {
  console.log('Account added successfully:', addedPair.address);
};

const onError = (errorMessage) => {
  console.error('Account subscription error:', errorMessage);
};

const onTransferSuccess = (transferData) => {
  console.log('Transfer completed successfully:', transferData);
  isTransferSuccess.value = true
};

const onTransferError = (errorMessage) => {
  console.error('Transfer error:', errorMessage);
};

watch(
  () => store.state?.robonomicsUIvue?.polkadot?.generatedAddress,
  (newVal) => {
    recipient.value = newVal
  }
);

</script>

<style scoped>
.flex-container {
  flex-direction: column;
}

code {
  background-color: var(--robo-color-bg-secondary, #f5f5f5);
  padding: 0.25rem;
  border-radius: 0.25rem;
  font-size: 0.875rem;
}

pre {
  margin: 0;
  white-space: pre-wrap;
  word-break: break-word;
}
</style>