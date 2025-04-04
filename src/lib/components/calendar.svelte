<script module>
    import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';

    export let plugins = [TimeGrid];
    export let options = $state({
        view: 'timeGridWeek',
        editable: true,
        styles: 'font-size: 24px; border-radius: 4px',
    });

    options.events = [
        {id: 1, start: '2025-3-24 7:00', end: '2025-3-24 17:00', display: 'auto', title: 'Work Day'},
            {id: 2, start: '2025-3-25 12:00', end: '2025-3-25 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange'},
            {id: 3, start: '2025-3-26 7:00', end: '2025-3-26 17:00', display: 'auto', title: 'Work Day'},
            {id: 4, start: '2025-3-27 12:00', end: '2025-3-27 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange'},
            {id: 5, start: '2025-3-28 7:00', end: '2025-3-28 14:00', allDay: true, display: 'auto', title: 'Vacation', backgroundColor:'purple'},
        {id: 11, start: '2025-3-10 7:00', end: '2025-3-10 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
        {id: 10, start: '2025-3-11 7:00', end: '2025-3-11 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
    ];

    export function updateOptions() { 
        //  options.slotDuration = '01:00'; 
        //  alert('hey');
         options.events = [
        // 10/21 - 10/25
            // {id: 1, start: '2025-3-3 7:00', end: '2025-3-3 17:00', display: 'background', title: 'Work Day'},
            // {id: 2, start: '2025-3-4 12:00', end: '2025-3-4 14:00', display: 'background', title: 'Lunch', backgroundColor: 'orange'},
            // {id: 3, start: '2025-3-5 7:00', end: '2025-3-5 17:00', display: 'background', title: 'Work Day'},
            // {id: 4, start: '2025-3-6 12:00', end: '2025-3-6 14:00', display: 'background', title: 'Lunch', backgroundColor: 'orange'},
            // {id: 5, start: '2025-3-7 7:00', end: '2025-3-7 14:00', allDay: true, display: 'background', title: 'Vacation', backgroundColor:'purple'},
            {id: 1, start: '2025-3-24 7:00', end: '2025-3-24 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
            {id: 2, start: '2025-3-25 12:00', end: '2025-3-25 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'grey'},
            {id: 3, start: '2025-3-26 7:00', end: '2025-3-26 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
            {id: 4, start: '2025-3-27 12:00', end: '2025-3-27 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'grey'},
            {id: 5, start: '2025-3-28 7:00', end: '2025-3-28 14:00', allDay: true, display: 'auto', title: 'Vacation', backgroundColor: 'grey'},
        ];
    }

    export function acceptOptions() {
        options.events = [
        // 10/21 - 10/25
            {id: 1, start: '2025-3-24 7:00', end: '2025-3-24 17:00', display: 'auto', title: 'Work Day'},
            {id: 2, start: '2025-3-25 12:00', end: '2025-3-25 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange'},
            {id: 3, start: '2025-3-26 7:00', end: '2025-3-26 17:00', display: 'auto', title: 'Work Day'},
            {id: 4, start: '2025-3-27 12:00', end: '2025-3-27 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange'},
            {id: 5, start: '2025-3-28 7:00', end: '2025-3-28 14:00', allDay: true, display: 'auto', title: 'Vacation', backgroundColor:'purple'},
        ];
    }

</script>