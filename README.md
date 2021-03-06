# Andreu - EA3IFH - DAB Transmitting PoC with HackRF and OpenRadioTools under Linux.

### Quick guide for personal use that worked me. 
### Have a look at their docs and their PDF (http://opendigitalradio.github.io/mmbtools-doc/mmbtools.pdf)


1) Have ODR tools installed. They supply a script for Debian/Ubuntu. https://github.com/Opendigitalradio

2) Create FIFOs

`mkfifo sortida.raw`

`mkfifo ofdm.fifo`

3) Get MP3 streaming (or a MP3 file) and publish it via localhost network.

`odr-audioenc -b 88 -v http://iscle359fm.cat:8880/iscle359.mp3 -e tcp://localhost:9000`

4) ODR-Dabmux will get that streaming and will create the MUX. More streamings can be fit into the Ensemble (use i.e. port 9001, 9002, etc).

`odr-dabmux iscle359dab.mux`

5) ODR-Dabmod will get that fifo (sortida.raw) and convert it to a OFDM stream ready to broadcast

`odr-dabmod iscle359fm.ini`

6) Broadcast that OFDM stream (216,928 is 11A)

`hackrf_transfer -t ofdm.fifo -f 216928000 -x 47 -s 4096000 -b 1750000`

https://twitter.com/ea3ifh/status/1407331447464136722?s=20
