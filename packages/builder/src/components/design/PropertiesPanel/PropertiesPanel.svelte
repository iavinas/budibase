<script>
  import { store, selectedComponent } from "builderStore"
  import { Tabs, Tab } from "@budibase/bbui"
  import ScreenSettingsSection from "./ScreenSettingsSection.svelte"
  import ComponentSettingsSection from "./ComponentSettingsSection.svelte"
  import DesignSection from "./DesignSection.svelte"
  import CustomStylesSection from "./CustomStylesSection.svelte"
  import ConditionalUISection from "./ConditionalUISection.svelte"

  $: componentInstance = $selectedComponent
  $: componentDefinition = store.actions.components.getDefinition(
    $selectedComponent?._component
  )
</script>

<Tabs selected="Settings" noPadding>
  <Tab title="Settings">
    <div class="container">
      {#key componentInstance?._id}
        <ScreenSettingsSection {componentInstance} {componentDefinition} />
        <ComponentSettingsSection {componentInstance} {componentDefinition} />
        <DesignSection {componentInstance} {componentDefinition} />
        <CustomStylesSection {componentInstance} {componentDefinition} />
        <ConditionalUISection {componentInstance} {componentDefinition} />
      {/key}
    </div>
  </Tab>
</Tabs>

<style>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: stretch;
  }
</style>
