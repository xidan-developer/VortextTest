<script>


    import { onMount } from 'svelte';

    import { Router, Route, Link } from "svelte-routing";
    import EventLocal from "../routes/EventLocal.svelte";

    let showMenu = false
    let selectedValue = ""

    function toggleMenu() {
        showMenu = !showMenu
    }



    let isLoading = false;
    let eventNameFilter = '';
    let locationFilter = '';
    $: items = [];
    $: uniqueLocations = [];
    let error = null;
    onMount(async () => {
        isLoading = true;

        try {
            const list = await fetch('https://events.vortex.foundation/events');

            if (!list.ok) {
                throw new Error('Ошибка при получении данных');
            }

            let response = await list.json();
            items = Array.isArray(response.data) ? response.data : [response.data];
            console.log(items)
            let location = Array.isArray(response.data) ? response.data : [response.data];
            const flattenedLocations = [].concat(...location);
            uniqueLocations = Array.from(new Set(flattenedLocations));
            error = null;
        } catch (err) {
            error = err.message;
            items = [];
            location = [];
        } finally {
            isLoading = false;
        }
    });
    const date = (dates) => {
        let dateStr = dates;
        let dateObj = new Date(dateStr);
        let options = { year: 'numeric', month: 'long', day: 'numeric' };
        let formattedDate = dateObj.toLocaleDateString('en-US', options);
        return formattedDate;
    }
    function handleInputChange(event) {
        eventNameFilter = event.target.value;
    }
    function handleLocationChange(event) {
        locationFilter = event.target.value;
    }
    function selectItem(event) {
        selectedValue = event.target.getAttribute("data-value")
        locationFilter = selectedValue
        showMenu = false
    }
    function trimString(trimString){
        return trimString.replace(/\s/g, "")
    }

</script>
<Router>
    <div class="title">
        <div class="container">
            <div class="title-1">Сalendar</div>
        </div>
    </div>
    <div class="search d-flex align-items-center justify-between">

        <input class="search__text" type="text" value="{eventNameFilter}" on:input="{handleInputChange}">

        <div class="relative">
            <div class="search__drop" on:click={toggleMenu} data-value="{locationFilter}" on:change="{handleLocationChange}">
                <div class="search__name">
                    {selectedValue !== "" ? selectedValue : 'All'}
                </div>
            </div>
            {#if showMenu}
                <div class="search_menu">
                    {#if isLoading}
                        <p>Загрузка данных...</p>
                    {:else if error}
                        <p>Ошибка: {error}</p>
                    {:else}
                            <div class="search_menu__item" data-value="" on:click={selectItem}>All</div>
                        {#each uniqueLocations as event}
                            <div class="search_menu__item" data-value="{event.location}" on:click={selectItem}>{event.location}</div>
                        {/each}

                    {/if}
                </div>
            {/if}
        </div>

    </div>
    <div class="table">
        <table class="table_list">
            <thead>
                <tr>
                    <th>Date</th>
                    <th>Event name</th>
                    <th>Location</th>
                </tr>
            </thead>
            <tbody>
            {#if isLoading}
                <p>Loading...</p>
            {:else if error}
                <p>Error: {error}</p>
            {:else}
                {#each items.filter(event => event.title.toLowerCase().includes(eventNameFilter.toLowerCase()) && event.location.toLowerCase().includes(locationFilter.toLowerCase())) as event}
                    <Link class="table_list__url" to="/{trimString(event.title)}">
                        <tr>
                            <td>
                                <div class="table_list--date">
                                    {
                                        date(event.date_start)
                                    }
                                </div>

                            </td>
                            <td>
                                <div>
                                    {event.title}
                                </div>
                            </td>
                            <td>
                                <div>
                                    {event.location}
                                </div>
                            </td>
                        </tr>
                    </Link>
                    <Route path="/{trimString(event.title)}" component={EventLocal}  id="{event}" />
                {/each}
            {/if}
            {#if isLoading}
                {#each items as event}
                    <Route path="/{trimString(event.title)}" component={EventLocal}  id="{event}" />
                {/each}
            {/if}
            </tbody>
        </table>
    </div>
</Router>







<style lang="sass">
    .title
      margin-top: 40px
  .search
    margin-top: 40px
    &__name
      text-overflow: ellipsis
      width: 140px
      overflow: hidden
      white-space: pre
    &_menu
      position: absolute
      top: 60px
      border: 1px solid #e6e6eb
      border-radius: 12px
      width: 100%
      background: white
      &__item
        padding: 14px 24px
        cursor: pointer
        &:hover
          background: #6a42e9
          color: white
        &:first-child
          border-radius: 12px 12px 0 0
        &:last-child
          border-radius: 0 0 12px 12px
    &__text
      margin-right: 28px
      border: 1px solid #e6e6eb
      padding: 17px 18px 15px 48px
      background: left center no-repeat
      background-position-x: 10px
      width: 100%
      font-size: 19px
      border-radius: 12px
      background-image: url("/img/search_icon.png")
      background-size: 34px

    &__drop
      position: relative
      width: 200px
      cursor: pointer
      border: 1px solid #e6e6eb
      padding: 17px 18px 15px
      border-radius: 12px
      &:after
        width: 24px
        height: 24px
        position: absolute
        right: 19px
        top: 50%
        transform: translate(0px, -50%)
        background-image: url("/img/drop_arrow.png")
        z-index: 1
        content: ""
        transition: .3s

  .table
    margin-top: 40px
    &_list
      background: #fff
      box-shadow: 0 5px 50px -10px rgba(40,51,78,.2)
      border-radius: 14px
      border-collapse: collapse
      width: 100%
      &--date
        color: #6a42e9
      thead
        border-bottom: 1px solid #0000000a
      tbody tr
        cursor: pointer
        td:first-child
          width: 400px
        &:hover
            background: #6a42e914
      th
        text-align: left
        color: #6a42e9
      th,td
        text-align: left
        padding: 25px 28px 21px
</style>