<script>
  import TextInput from "../inputs/text-input.svelte";
  import { language } from "../../stores/language";
  import { Language } from "../../pages/types";
  import Select from "../select/select.svelte";
  import { writable } from "svelte/store";

  const languages = Object.entries(Language)
    .filter(([key]) => !(Number(key) >= 0))
    .map(([key, language]) => ({
      name: key,
      language,
    }));

  const selectedLanguage = writable(language.get());

  selectedLanguage.subscribe((newLanguage) => {
    language.set(newLanguage?.language ?? language.get());
  });
</script>

<div class="flex header-wrapper align-center">
  <header>
    <nav class="flex space-between">
      <div class="logo">DASM</div>
      <div class="flex gap-20">
        <Select
          options={languages}
          displayFunction={(option) => option.name}
          index={language.get()}
          bind:value={$selectedLanguage}
        />
        <TextInput type="text" placeholder="Search">
          <svg
            width="20px"
            height="20px"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M20 20L15.8033 15.8033M18 10.5C18 6.35786 14.6421 3 10.5 3C6.35786 3 3 6.35786 3 10.5C3 14.6421 6.35786 18 10.5 18C14.6421 18 18 14.6421 18 10.5Z"
              stroke="#fff"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </TextInput>
      </div>
    </nav>
  </header>
</div>

<style>
  .header-wrapper {
    width: 100%;
    height: 60px;
    border-bottom: 1px solid #757575;
  }

  .header-wrapper header {
    width: 100%;
  }

  .header-wrapper nav {
    padding-inline: 10%;
  }

  .header-wrapper .logo {
    font-size: 25px;
  }
</style>
