# synth-protos

_The proto files to define the sysex messages the synth show uses_

## Handshake Messages

There are 3 messages that define the handshake sequence:

- **SYN**  
   Sent by the Sequencer when brought on-line
- **SYNACK**  
   Sent by a peripheral in response to an incoming SYN or when brought it is on-line
- **ACK**  
   Sent by the Sequencer in response to a SYNACK message, followed by data transfer

### If the Sequencer is the second one to come on-line

```
Sequencer    Peripheral
    |            |
    |        [Power on]
    |            |
    |<--SYN ACK--|
    |            |
[Power on]       |
    |            |
    |----SYN---->|
    |            |
    |<--SYN ACK--|
    |            |
    |----ACK---->|
    |            |
    |<---DATA--->|
    |            |
```

### If the peripheral is the second one to come on-line

```
Sequencer    Peripheral
    |            |
[Power on]       |
    |            |
    |----SYN---->|
    |            |
    |        [Power on]
    |            |
    |<--SYN ACK--|
    |            |
    |----ACK---->|
    |            |
    |<---DATA--->|
    |            |
```

## Control Requests

The control requests style a control on a MIDI Controller  
Controls have a static prefix, dynamic value, and static suffix

### Range Controls

A range control's dynamic value is determined by mapping the knob's range onto a minimum and maximum value  
The knob itself has 7-bits of resolution, so large min-max ranges will result in skipped values due to lack of precision

### Option Controls

An option control's dynamic value is determined by mapping the knob's range onto a list of strings
The number of strings in the list cannot exceed the number of different values you can have with 7-bits

## TO DO

- Transporter State
  - Chart Title
  - Button Lit State
  - Error Indicator
- MIDI to CV
  - Portamento
  - Retrigger Mode
  - Note Priority
