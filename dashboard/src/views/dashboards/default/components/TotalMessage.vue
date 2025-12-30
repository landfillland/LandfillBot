<template>
  <item-card :item="stat" class="stat-card message-card stat-item-card" :hide-header="true">
    <template #item-details="{ item }">
      <div class="d-flex align-start">
        <div class="icon-wrapper">
          <v-icon icon="mdi-message-text-outline" size="24"></v-icon>
        </div>

        <div class="stat-content">
          <div class="stat-title">{{ t('stats.totalMessage.title') }}</div>
          <div class="stat-value-wrapper">
            <h2 class="stat-value">{{ formattedCount }}</h2>
            <v-chip v-if="stat.daily_increase" class="trend-chip" size="x-small" color="success" variant="flat">
              +{{ stat.daily_increase }}
            </v-chip>
          </div>
          <div class="stat-subtitle">{{ t('stats.totalMessage.subtitle') }}</div>
        </div>
      </div>
    </template>
  </item-card>
</template>

<script>
import { useModuleI18n } from '@/i18n/composables';
import ItemCard from '@/components/shared/ItemCard.vue';

export default {
  name: 'TotalMessage',
  components: { ItemCard },
  props: ['stat'],
  setup() {
    const { tm: t } = useModuleI18n('features/dashboard');
    return { t };
  },
  computed: {
    formattedCount() {
      const count = this.stat?.message_count;
      return count ? count.toLocaleString() : '0';
    }
  }
};
</script>

<style scoped>
.stat-card {
  height: 100%;
  transition: transform 0.2s, box-shadow 0.2s;
  overflow: hidden;
}

.stat-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08) !important;
}

.message-card {
  border: 5px solid rgb(var(--v-theme-primary));
  color: rgb(var(--v-theme-primary));
}

.stat-item-card ::v-deep .v-card-title,
.stat-item-card ::v-deep .v-card-actions {
  display: none;
}

.icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 8px;
  margin-right: 16px;
  background: rgba(var(--v-theme-primary), 0.1);
  color: rgb(var(--v-theme-primary));
}

.stat-content {
  flex: 1;
}

.stat-title {
  font-size: 14px;
  font-weight: 500;
  opacity: 0.9;
  margin-bottom: 4px;
}

.stat-value-wrapper {
  display: flex;
  align-items: baseline;
  margin-bottom: 4px;
}

.stat-value {
  font-size: 32px;
  font-weight: 600;
  line-height: 1.2;
  margin-right: 8px;
}

.trend-chip {
  font-weight: 600;
}

.stat-subtitle {
  font-size: 12px;
  opacity: 0.7;
}
</style>