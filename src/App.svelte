<script>
  /**
   * USED FOR DEVELOPMENT OF COMPONENT ONLY.
   *
   * Using a svelte wrapper component to manage state allows for svelte-style
   * reactivity, rather than using foobar.$on() and foobar.$set()
   */
  import { endOfWeek, startOfWeek, startOfDay, endOfDay } from "date-fns";
  import * as locales from "date-fns/locale";
  import SDateRangePicker from "./date-range-picker/SDateRangePicker.svelte";

  const random = false;

  const localesArray = Object.keys(locales).map(i => locales[i]);
  const locale = random
    ? localesArray[Math.floor(Math.random() * localesArray.length)]
    : undefined;
  const singlePicker = false;
  let startDate = singlePicker
    ? startOfDay(new Date())
    : startOfWeek(new Date());
  let endDate = singlePicker ? startDate : endOfWeek(new Date());
  let monthDropdown = random ? Boolean(Math.floor(Math.random() * 2)) : true;
  let yearDropdown = random ? Boolean(Math.floor(Math.random() * 2)) : true;
  let todayBtn = random ? Boolean(Math.floor(Math.random() * 2)) : true;
  let resetViewBtn = random ? Boolean(Math.floor(Math.random() * 2)) : true;

  function onApply({ detail }) {
    startDate = detail.startDate;
    endDate = detail.endDate;
    console.log("apply", detail);
  }
  function onSubmit() {
    console.log("onSubmit");
  }
</script>

<SDateRangePicker
  {singlePicker}
  {monthDropdown}
  {yearDropdown}
  {resetViewBtn}
  {todayBtn}
  {locale}
  {startDate}
  {endDate}
  on:apply={onApply} />

<form on:submit|preventDefault={onSubmit}>
  <input type="text" />
  <button>submit</button>
</form>
