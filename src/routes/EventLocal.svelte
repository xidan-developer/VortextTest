<script>
    export let id
    console.log(id)
    function formatDateRange(startDate, endDate) {
        let monthNames = ["January", "February", "March", "April", "May", "June",
            "July", "August", "September", "October", "November", "December"
        ];
        startDate = new Date(startDate)
        endDate = new Date(endDate)
        let startDay = startDate.getDate();
        let startMonthIndex = startDate.getMonth();
        let startYear = startDate.getFullYear();

        let endDay = endDate.getDate();
        let endMonthIndex = endDate.getMonth();
        let endYear = endDate.getFullYear();

        let dateRange =  startDay + '-' + endDay + ' ' + monthNames[startMonthIndex] + ' ' + startYear;
        if (startYear !== endYear || startMonthIndex !== endMonthIndex) {
            dateRange += ' ' + startYear;
        }
        return dateRange;
    }

    function load() {
        history.go(-1);
        return false;
    }

</script>

<div class="modal-overflow">
    <div class="modal">
        <div class="modal__close" on:click={() => load()}></div>
        <div class="d-flex modal_row align-items-center">
            <img class="modal_row__preview" src="img/event-taipeiblockchainweek-d58055.jpg" alt="">
            <div class="modal_row__title">{id.title}</div>
        </div>
        <div class="modal_date">
            <div class="modal_date__value d-flex align-items-start justify-between">
                <div>
                    Time event:
                    <span class="modal_date__color">

                        {
                            formatDateRange(id.date_start,id.date_end)
                        }
                    </span>
                </div>
                <div>
                    {id.location}
                </div>
            </div>
        </div>
        <div class="modal_description">
            {id.description}
        </div>
        <a class="modal__url" href="#">Visit event's</a>
    </div>
</div>

<style lang="sass">
    .overflow-hidden
      overflow: hidden

    .modal-overflow
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100vh
      background: rgba(0,0,0,.5)
      display: flex
    .modal
      width: 774px
      padding: 40px
      margin: 100px auto auto
      background: #fff
      box-shadow: 0 5px 50px -10px rgba(40,51,78,.2)
      border-radius: 14px
      position: relative
      &__close
        position: absolute
        right: 28px
        top: 28px
        cursor: pointer
        width: 20px
        height: 20px
        background-image: url("/img/close.png")
        background-size: contain
      &__url
        color: #6a42e9
        margin-top: 30px
        display: block
      &_date
        margin-top: 30px
        &__color
          color: #6a42e9
      &_description
        margin-top: 30px
      &_row
        gap: 50px
        &__title
          font-size: 26px
          margin: auto

</style>