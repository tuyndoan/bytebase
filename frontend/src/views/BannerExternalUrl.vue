<template>
  <div v-if="show" class="bg-accent">
    <div class="mx-auto py-3 px-3">
      <div class="flex items-center justify-between flex-wrap">
        <div class="w-0 flex-1 flex items-center">
          <p class="ml-3 font-medium text-white truncate">
            <span>
              {{ $t("banner.external-url") }}
            </span>
          </p>
        </div>
        <div
          v-if="hasPermission"
          class="order-3 mt-2 flex-shrink-0 w-full sm:order-2 sm:mt-0 sm:w-auto"
        >
          <router-link
            :to="{ name: SETTING_ROUTE_WORKSPACE_GENERAL }"
            class="flex items-center justify-center pl-4 pr-2 py-2 border border-transparent rounded-md shadow-sm text-base font-medium text-accent bg-white hover:bg-indigo-50"
          >
            {{ $t("common.configure-now") }}
            <heroicons-outline:wrench-screwdriver class="ml-1 w-5 h-5" />
          </router-link>
        </div>
        <div class="order-2 flex-shrink-0 sm:order-3 sm:ml-3 -mr-1">
          <NButton quaternary size="small" @click.prevent="show = false">
            <span class="sr-only">{{ $t("common.dismiss") }}</span>
            <template #icon>
              <!-- Heroicon name: outline/x -->
              <heroicons-outline:x class="h-6 w-6 text-white" />
            </template>
          </NButton>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { NButton } from "naive-ui";
import { ref, computed } from "vue";
import { SETTING_ROUTE_WORKSPACE_GENERAL } from "@/router/dashboard/workspaceSetting";
import { hasWorkspacePermissionV2 } from "@/utils";

const show = ref(true);

const hasPermission = computed(() =>
  hasWorkspacePermissionV2("bb.settings.set")
);
</script>
