flowchart TD
    Start([Patient Requests Reschedule]) --> SelectSlot[Select New Time Slot: 2026-10-16T14:00:00Z]
    SelectSlot --> CheckTime{Is request less than<br/>24 hours from original time?}

    CheckTime -- Yes --> ApplyFlag[Apply 'Late-Change' Flag]
    CheckTime -- No --> UpdateDB[Update Appointment Record]

    ApplyFlag --> UpdateDB
    UpdateDB --> EmitEvent[Emit 'AppointmentRescheduled' Event]
    
    EmitEvent --> AsyncNotify[Notification Service<br/>Sends Email/SMS]
    EmitEvent --> RenderUI[Display Confirmation UI with Updated Details]
    
    AsyncNotify --> End([Process Complete])
    RenderUI --> End
