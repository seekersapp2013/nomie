<script>
  // Vendors
  import { onMount } from "svelte";
  import { Link } from "svelte-routing";

  // Components
  import Icon from "../../components/icon/icon.svelte";

  import { Lang } from "../../store/lang";
  import { TrackerStore } from "../../store/tracker-store";

  const state = {
    mounted: false
  };

  onMount(() => {
    state.mounted = true;
  });
</script>

<style lang="scss">
  @import "../../scss/utils/__utils.scss";
  #app-tabs {
    height: calc(62px + env(safe-area-inset-bottom));
    padding-bottom: calc(env(safe-area-inset-bottom));
    background-color: var(--footer-background);
    display: flex;
    justify-content: space-between;
    align-items: stretch;
    z-index: 1200;
    flex-shrink: 0;

    .n-row {
      z-index: 10;
      max-height: 60px;
      min-height: 60px;
      height: 60px;
      flex-shrink: 0;
    }
    .notification {
      position: absolute;
      top: 0;
      right: calc(50% - 15px);
      width: 6px;
      height: 6px;
      background-color: var(--color-red);
      border-radius: 3px;
    }
  }

  :global(#app-tabs a svg) {
    height: 24px !important;
    width: 24px !important;
    margin-bottom: 3px;
  }

  :global(#app-tabs a[aria-current="page"] svg) {
    fill: var(--color-primary-bright) !important;
    transform: scale(1.1);
    transition: all 0.2s ease-in-out;
  }

  :global(#app-tabs a[aria-current="page"] svg .fill) {
    fill: var(--color-primary-bright) !important;
  }

  :global(#app-tabs a) {
    color: var(--color-inverse-2);
    display: inline-flex;
    flex-direction: column;
    align-items: center;
    position: relative;
    padding: 4px 10px 0;
    font-size: 0.7rem;
    text-decoration: none;
    // opacity: 0.6;
    transition: all 0.2s ease-in-out;
    min-width: 30px;
    width: 100%;
    i {
      font-size: 1.2rem;
      transition: all 0.2s ease-in-out;
    }
    label {
      margin-bottom: 0;
    }

    &:after {
      content: "";
      position: absolute;
      bottom: -6px;
      left: 40%;
      right: 40%;
      height: 0px;
      border-radius: 2px;
      background-color: rgba($primaryBright, 0);
    }

    // When Active
    &[aria-current="page"] {
      color: var(--color-primary-bright);
      svg {
        fill: var(--color-primary-bright);
        transform: scale(1.1);
        transition: all 0.2s ease-in-out;
      }
      &:after {
        content: "";
        position: absolute;
        bottom: -6px;
        left: 20%;
        right: 20%;
        height: 4px;
        border-radius: 2px;
        background-color: var(--color-primary-bright);
      }
    }
  }
</style>

{#if state.mounted}
  <nav id="app-tabs" class="">
    <div class="n-row mw-500px mx-auto">

      <Link to="/history">
        <Icon name="calendar" />
        <label>{Lang.t('tabs.history')}</label>
      </Link>

      <Link to="/">
        {#if $TrackerStore.timers.length}
          <div class="notification" />
        {/if}
        <Icon name="tracker" />
        <label>{Lang.t('general.trackers', 'Trackers')}</label>
      </Link>

      <Link to="/people">
        <Icon name="people" />
        <label>{Lang.t('tabs.people')}</label>
      </Link>

      <Link to="/settings">
        <Icon name="settings" />
        <label>{Lang.t('tabs.settings')}</label>
      </Link>

    </div>
  </nav>
{/if}
