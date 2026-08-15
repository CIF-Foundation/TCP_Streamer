# TCP_Streamer
TCP unidirectional streamer to support loose coupling between sender and receiver to provide high reliability for both sender and receiver and is agnostic to payload.  
All calls are designed to have short timeouts to assure applications remain responsive to other commands (such as to reconfigure or shut down).

Data Sender:
- Data sender will create TCP listener
- On connection it will stream payload 
- If the write times out due to full buffers it will indicate a timeout and track payload bytes sent
- On the next iteration it will resume sending the buffer
- On connection terminated it will re-open listener

Data Receiver
- Data receiver will connect to TCP listener
- Will receive payload stream
- On connection terminated it will attempt to connect to listener
