# Classes, Arguments, and Methods

## Classes

W3XDE only contains two classes. (well, for actual use!) The `CentralServer` and the `TrainingNode`.

### CentralServer

The `CentralServer` class is the central hub for all training data. It's responsible for distributing batches to all connected `TrainingNode` instances, and aggregating gradients from them.

#### Arguments

- `model` The model to train. Must be a PyTorch model class.
- `dataset` The dataset to train on. Must be a PyTorch dataset class.
- `batch_size` The size of the batches to distribute. Default is 16.
- `ip` The IP address to bind the server to. Default is "localhost". ("0.0.0.0" for all interfaces)
- `port` The port to bind the server to. Default is 5555.
- `secure` Whether or not to use encryption. Default is False. Encryption drastically slows down training, so only use it if you need to. (like, really need to)
  
#### Methods
- `start()` Starts the server. This is a blocking call, so it will not return until the server is stopped. 
  
### TrainingNode

The `TrainingNode` class is the client that connects to the `CentralServer` to receive batches and send gradients.

#### Arguments

- `model` The model to train. Must be a PyTorch model class.
- `secure` Whether or not to use encryption. Default is False. Encryption drastically slows down the submission of gradients, so only use it if you need to. (like, really need to)

#### Methods
- `train()` Starts training the model. This is a blocking call, so it will not return until training is complete.