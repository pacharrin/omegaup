<template>
  <div>
    <form
      class="form add-identity-form"
      @submit.prevent="$emit('add-identity', { username, password })"
    >
      <div class="form-group">
        <label class="w-100">
          {{ T.wordsIdentity }}
          <font-awesome-icon
            :title="T.profileAddIdentitiesTooltip"
            icon="info-circle"
          ></font-awesome-icon>
          <input
            v-model="username"
            autocomplete="off"
            class="form-control username-input"
            size="20"
            type="text"
          />
        </label>
      </div>
      <div class="form-group">
        <label class="w-100">
          {{ T.loginPassword }}
          <input
            v-model="password"
            autocomplete="off"
            class="form-control password-input"
            size="20"
            type="password"
          />
        </label>
      </div>
      <div class="form-group text-right">
        <button class="btn btn-primary" type="submit">
          {{ T.wordsAddIdentity }}
        </button>
      </div>
    </form>
    <div v-if="identities.length == 0">
      <div class="empty-category">
        {{ T.profileIdentitiesEmpty }}
      </div>
    </div>
    <table v-else class="table table-striped table-over">
      <thead>
        <tr>
          <th>{{ T.wordsIdentity }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="identity in identities" :key="identity.username">
          <td>{{ identity.username }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import { types } from '../../api_types';
import T from '../../lang';

import {
  FontAwesomeIcon,
  FontAwesomeLayers,
  FontAwesomeLayersText,
} from '@fortawesome/vue-fontawesome';
import { fas } from '@fortawesome/free-solid-svg-icons';
import { library } from '@fortawesome/fontawesome-svg-core';
library.add(fas);

@Component({
  components: {
    'font-awesome-icon': FontAwesomeIcon,
    'font-awesome-layers': FontAwesomeLayers,
    'font-awesome-layers-text': FontAwesomeLayersText,
  },
})
export default class ManageIdentities extends Vue {
  @Prop() identities!: types.Identity[];

  T = T;
  username = '';
  password = '';
}
</script>
