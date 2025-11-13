# In-Class Assignment - Neural Networks with TensorFlow
## Building and Training Neural Networks Using TensorFlow/Keras

**Objective**: Learn to build, train, and evaluate neural networks using TensorFlow and Keras.

---

## Setup

```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers, models
from sklearn.datasets import make_moons, make_circles
from sklearn.model_selection import train_test_split

# Set random seeds for reproducibility
np.random.seed(42)
tf.random.set_seed(42)

# Check TensorFlow version
print(f"TensorFlow version: {tf.__version__}")
print(f"GPU Available: {tf.config.list_physical_devices('GPU')}")
```

---

## Part 1: Understanding Activation Functions

### 1.1: Explore Built-in Activation Functions

```python

x = np.linspace(-5, 5, 200)

# Create figure
plt.figure(figsize=(15, 10))

# ReLU
plt.subplot(2, 3, 1)
y_relu = tf.nn.relu(x).numpy()
plt.plot(x, y_relu, 'r-', linewidth=2)
plt.title('ReLU Activation', fontsize=14, fontweight='bold')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.ylabel('Output')

# Sigmoid
plt.subplot(2, 3, 2)
y_sigmoid = tf.nn.sigmoid(x).numpy()
plt.plot(x, y_sigmoid, 'g-', linewidth=2)
plt.title('Sigmoid Activation', fontsize=14, fontweight='bold')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)

# Tanh
plt.subplot(2, 3, 3)
y_tanh = tf.nn.tanh(x).numpy()
plt.plot(x, y_tanh, 'b-', linewidth=2)
plt.title('Tanh Activation', fontsize=14, fontweight='bold')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)

# Leaky ReLU
plt.subplot(2, 3, 4)
y_leaky = tf.nn.leaky_relu(x, alpha=0.2).numpy()
plt.plot(x, y_leaky, 'purple', linewidth=2)
plt.title('Leaky ReLU (α=0.2)', fontsize=14, fontweight='bold')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.xlabel('Input')
plt.ylabel('Output')

# ELU
plt.subplot(2, 3, 5)
y_elu = tf.nn.elu(x).numpy()
plt.plot(x, y_elu, 'orange', linewidth=2)
plt.title('ELU Activation', fontsize=14, fontweight='bold')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.xlabel('Input')

# Comparison
plt.subplot(2, 3, 6)
plt.plot(x, y_relu, 'r-', label='ReLU', linewidth=2, alpha=0.7)
plt.plot(x, y_sigmoid, 'g-', label='Sigmoid', linewidth=2, alpha=0.7)
plt.plot(x, y_tanh, 'b-', label='Tanh', linewidth=2, alpha=0.7)
plt.plot(x, y_leaky, 'purple', label='Leaky ReLU', linewidth=2, alpha=0.7)
plt.title('Comparison', fontsize=14, fontweight='bold')
plt.legend()
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.xlabel('Input')

plt.tight_layout()
plt.show()

```

### 1.2: Test Your Understanding

```python
# Creating a small tensor and apply different activations
test_input = tf.constant([-2.0, -1.0, 0.0, 1.0, 2.0])

# TODO: Apply ReLU
relu_output = # YOUR CODE HERE
print("ReLU output:", relu_output.numpy())

# TODO: Apply Sigmoid
sigmoid_output = # YOUR CODE HERE
print("Sigmoid output:", sigmoid_output.numpy())

# ASSERTIONS
assert np.allclose(relu_output.numpy(), [0, 0, 0, 1, 2]), " ReLU output incorrect!"

assert np.isclose(sigmoid_output.numpy()[2], 0.5, atol=1e-6), " Sigmoid(0) should be 0.5!"

print("✓ Activation function tests passed!")
```

---

## Part 2: Building a Shallow Network with Keras

### 2.1: Sequential API - Building Block by Block

```python
def build_shallow_network(input_dim, hidden_dim, output_dim):
    """
    Build a shallow neural network using Keras Sequential API
    
    Args:
        input_dim: number of input features
        hidden_dim: number of hidden units
        output_dim: number of output units (1 for binary classification)
    
    Returns:
        model: compiled Keras model
    """
    # TODO: Create Sequential model
    model = # YOUR CODE HERE
    
    return model

# Create a shallow network
model = build_shallow_network(input_dim=2, hidden_dim=3, output_dim=1)

# Display model architecture
print("\n" + "="*70)
print("--- SHALLOW NETWORK ARCHITECTURE")
print("="*70)
model.summary()
```

### 2.2: Visualize Network Structure

```python
# TODO: Visualize the model architecture
# YOUR CODE HERE

print("\n✓ Model architecture saved to 'shallow_network.png'")

# Count parameters
total_params = model.count_params()
print(f"\nTotal Parameters: {total_params:,}")

# Break down by layer
print("\nParameters by Layer:")
for layer in model.layers:
    print(f"  {layer.name}: {layer.count_params():,} parameters")
```

### 2.3: Inspect Model Weights

```python
# Get weights from each layer
print("\n" + "="*70)
print(" WEIGHT SHAPES")
print("="*70)


# TODO: get weights and biases and print them
for layer in model.layers:
    # YOUR CODE HERE
    print(f"\n{layer.name}:")
    print(f"  Weights (W): {weights.shape}")
    print(f"  Biases (b):  {weights.shape}")

# ASSERTIONS
hidden_layer = model.get_layer('hidden_layer')
output_layer = model.get_layer('output_layer')

w1, b1 = hidden_layer.get_weights()
w2, b2 = output_layer.get_weights()

assert w1.shape == (2, 3), f"Hidden layer weights shape wrong! Got {w1.shape}"
assert b1.shape == (3,), f"Hidden layer bias shape wrong! Got {b1.shape}"
assert w2.shape == (3, 1), f"Output layer weights shape wrong! Got {w2.shape}"
assert b2.shape == (1,), f"Output layer bias shape wrong! Got {b2.shape}"

print("\n✓ All weight shape assertions passed!")
```

---

## Part 3: Understanding Model Compilation

### 3.1: Loss Functions in TensorFlow

```python
# Test different loss functions
y_true = tf.constant([[1.0], [0.0], [1.0], [0.0]])
y_pred_good = tf.constant([[0.9], [0.1], [0.85], [0.15]])
y_pred_bad = tf.constant([[0.1], [0.9], [0.2], [0.8]])

# TODO: Binary cross-entropy
bce = # YOUR CODE HERE
loss_good = # YOUR CODE HERE ( apply bce to y_true and y_pred_good and the convert the result to numpy array using .numpy() method )
loss_bad = # YOUR CODE HERE ( apply bce to y_true and y_pred_bad and the convert the result to numpy array using .numpy() method )

print(f"\n" + "="*70)
print("Loss Function Example:")
print(f"  Good predictions loss: {loss_good:.4f}")
print(f"  Bad predictions loss:  {loss_bad:.4f}")

# ASSERTION
assert loss_bad > loss_good, "Bad predictions should have higher loss!"

print("✓ Loss function test passed!")
```

### 3.2: Compile the Model

```python
# TODO: Compile the model with loss and metrics
model.compile(
    # YOUR CODE HERE
)

print("\n" + "="*70)
print("✓ Model compiled successfully!")
print("="*70)
```

---

## Part 4: Training the Network

### 4.1: Prepare Dataset

```python
# synthetic dataset generation
X, y = make_moons(n_samples=1000, noise=0.2, random_state=42)
X_train, X_val, y_train, y_val = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# plotting the data
plt.figure(figsize=(10, 6))
plt.scatter(X_train[y_train==0, 0], X_train[y_train==0, 1], 
           c='blue', label='Class 0', alpha=0.6, edgecolors='k')
plt.scatter(X_train[y_train==1, 0], X_train[y_train==1, 1], 
           c='red', label='Class 1', alpha=0.6, edgecolors='k')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.title('Training Dataset - Two Moons')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()

print(f"Training samples: {X_train.shape[0]}")
print(f"Test samples: {X_val.shape[0]}")
print(f"Features: {X_train.shape[1]}")
```

### 4.2: Train the Model

```python
print("\n" + "="*70)
print("TRAINING SHALLOW NETWORK")
print("="*70)

# TODO: define a NEW shallow model with 100 hidden units, 2 inputs and 1 output - REMEMBER to "compile" the model after creating it.
model = # YOUR CODE HERE

# TODO: Train the model
# fit the model using 50 epochs and bach_size of 64
history = # YOUR CODE HERE 

print("\n✓ Training completed!")
```

### 4.3: Visualize Training History

```python
# Ploting training history
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.plot(history.history['loss'], label='Train Loss', linewidth=2)
plt.plot(history.history['val_loss'], label='Val Loss', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Training and Validation Loss')
plt.legend()
plt.grid(True, alpha=0.3)

plt.subplot(1, 3, 2)
plt.plot(history.history['accuracy'], label='Train Accuracy', linewidth=2)
plt.plot(history.history['val_accuracy'], label='Val Accuracy', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.title('Training and Validation Accuracy')
plt.legend()
plt.grid(True, alpha=0.3)

plt.subplot(1, 3, 3)
# Learning curve
epochs = range(1, len(history.history['loss']) + 1)
plt.plot(epochs, history.history['val_accuracy'], 'b-', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Validation Accuracy')
plt.title('Learning Curve')
plt.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

# Print final results
final_train_loss = history.history['loss'][-1]
final_val_loss = history.history['val_loss'][-1]
final_train_acc = history.history['accuracy'][-1]
final_val_acc = history.history['val_accuracy'][-1]

print("\n" + "="*70)
print("TRAINING RESULTS")
print("="*70)
print(f"Final Training Loss:      {final_train_loss:.4f}")
print(f"Final Validation Loss:    {final_val_loss:.4f}")
print(f"Final Training Accuracy:  {final_train_acc:.2%}")
print(f"Final Validation Accuracy: {final_val_acc:.2%}")

# ASSERTION
assert final_val_acc > 0.75, \
    f"Validation accuracy too low! Got {final_val_acc:.2%}"

print("\n✓ Training performance assertion passed!")
```

---

## Part 5: Model Evaluation and Predictions

### 5.1: Make Predictions

```python
# Using model to make predictions
y_pred_proba = model.predict(X_val)
y_pred_classes = (y_pred_proba > 0.5).astype(int).flatten()

print("\nSample Predictions:")
print(f"True labels:      {y_val[:10]}")
print(f"Predicted probs:  {y_pred_proba.flatten()[:10]}")
print(f"Predicted class:  {y_pred_classes[:10]}")

# Evaluate on validation set
val_loss, val_acc = model.evaluate(X_val, y_val, verbose=0)
print(f"\n" + "="*70)
print(f"Validation Loss:     {val_loss:.4f}")
print(f"Validation Accuracy: {val_acc:.2%}")
print("="*70)
```

### 5.2: Confusion Matrix

```python
from sklearn.metrics import confusion_matrix, f1_score
import seaborn as sns

# Confusion matrix
cm = # YOUR CODE HERE

plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
            xticklabels=['Class 0', 'Class 1'],
            yticklabels=['Class 0', 'Class 1'])
plt.title('Confusion Matrix')
plt.ylabel('True Label')
plt.xlabel('Predicted Label')
plt.show()

# Fscore report
print("\n" + "="*70)
fscore = # YOUR CODE HERE
print(f"F Score {fscore:0.3f}")
```

### 5.3: Decision Boundary Visualization

```python
def plot_decision_boundary(model, X, y, title="Decision Boundary"):
    """Plot decision boundary for a 2D dataset"""
    x_min, x_max = X[:, 0].min() - 0.5, X[:, 0].max() + 0.5
    y_min, y_max = X[:, 1].min() - 0.5, X[:, 1].max() + 0.5
    
    xx, yy = np.meshgrid(np.linspace(x_min, x_max, 200),
                        np.linspace(y_min, y_max, 200))
    
    # Make predictions on mesh
    mesh_input = np.c_[xx.ravel(), yy.ravel()]
    Z = model.predict(mesh_input, verbose=0)
    Z = Z.reshape(xx.shape)
    
    # Plot
    plt.figure(figsize=(10, 8))
    plt.contourf(xx, yy, Z, levels=20, cmap='RdYlBu', alpha=0.6)
    plt.colorbar(label='Predicted Probability')
    
    plt.scatter(X[y==0, 0], X[y==0, 1], c='blue', 
               label='Class 0', edgecolors='k', s=50)
    plt.scatter(X[y==1, 0], X[y==1, 1], c='red', 
               label='Class 1', edgecolors='k', s=50)
    
    plt.xlabel('Feature 1')
    plt.ylabel('Feature 2')
    plt.title(title)
    plt.legend()
    plt.show()

# Plot decision boundary
plot_decision_boundary(model, X_val, y_val, 
                      title="Shallow Network (2→100→1)")
```

---

## Part 6: Optimizers and Learning Rate

### 6.1: Compare Different Optimizers

```python
# Test different optimizers
optimizers_to_test = {
    'SGD': keras.optimizers.SGD(learning_rate=0.01),
    'SGD + Momentum': keras.optimizers.SGD(learning_rate=0.01, momentum=0.9),
    'RMSprop': keras.optimizers.RMSprop(learning_rate=0.001),
    'Adam': keras.optimizers.Adam(learning_rate=0.001)
}

results = {}

for optimizer_name, optimizer in optimizers_to_test.items():
    print(f"\nTraining with {optimizer_name}...")
    
    # Build new model
    model_test = build_shallow_network(2, 10, 1)
    model_test.compile(
        optimizer=optimizer,
        loss='binary_crossentropy',
        metrics=['accuracy']
    )
    
    # Train
    history = model_test.fit(
        X_train, y_train,
        validation_data=(X_val, y_val),
        epochs=50,
        batch_size=32,
        verbose=0
    )
    
    results[optimizer_name] = history.history

# Plot comparison
plt.figure(figsize=(15, 5))

plt.subplot(1, 2, 1)
for name, hist in results.items():
    plt.plot(hist['loss'], label=name, linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Training Loss')
plt.title('Optimizer Comparison - Training Loss')
plt.legend()
plt.grid(True, alpha=0.3)

plt.subplot(1, 2, 2)
for name, hist in results.items():
    plt.plot(hist['val_accuracy'], label=name, linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Validation Accuracy')
plt.title('Optimizer Comparison - Validation Accuracy')
plt.legend()
plt.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

```

---

## Part 7: Building Deep Networks

### 7.1: Create a Deep Network

```python
def build_deep_network(layer_dims):
    """
    Build a deep neural network
    
    Args:
        layer_dims: list of layer dimensions [input, hidden1, hidden2, ..., output]
    
    Returns:
        model: Keras model
    """
    model = models.Sequential()
    
    # input layer
    model.add(layers.Input(shape=(layer_dims[0],)))
    
    # hidden layers (all but last)
    for i, units in enumerate(layer_dims[1:-1], 1):
        model.add(layers.Dense(units, activation='relu', name=f'hidden_{i}'))
    
    # output layer
    model.add(layers.Dense(layer_dims[-1], activation='sigmoid', name='output'))
    
    return model

# Create deep network
deep_model = build_deep_network([2, 10, 10, 1])

print("\n" + "="*70)
print("DEEP NETWORK ARCHITECTURE")
print("="*70)
deep_model.summary()

# Visualize architecture
tf.keras.utils.plot_model(
    deep_model,
    to_file='deep_network.png',
    show_shapes=True,
    show_layer_names=True,
    rankdir='TB',
    expand_nested=True,
    dpi=96
)

print("\n✓ Deep network architecture saved to 'deep_network.png'")
```

### 7.2: Compare Network Architectures

```python
# multiple architectures
architectures = {
    'Shallow (2→10→1)': [2, 10, 1],
    'Deep (2→10→10→1)': [2, 10, 10, 1],
    'Deeper (2→20→15→10→1)': [2, 20, 15, 10, 1],
    'Wide (2→50→1)': [2, 50, 1]
}

print("\n" + "="*70)
print("ARCHITECTURE COMPARISON")
print("="*70)

for name, dims in architectures.items():
    model_temp = build_deep_network(dims)
    total_params = model_temp.count_params()
    depth = len(dims) - 1
    width = max(dims[1:-1]) if len(dims) > 2 else dims[1]
    
    print(f"\n{name}:")
    print(f"  Depth (layers):      {depth}")
    print(f"  Width (max units):   {width}")
    print(f"  Total parameters:    {total_params:,}")
```

---

## Part 8: Training Deep Networks

### 8.1: Train Deep Network

```python
# deep model
deep_model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)

print("\n" + "="*70)
print("TRAINING DEEP NETWORK")
print("="*70)

# Train with early stopping and learning rate reduction
callbacks = [
    keras.callbacks.EarlyStopping(
        monitor='val_loss',
        patience=20,
        restore_best_weights=True,
        verbose=1
    ),
    keras.callbacks.ReduceLROnPlateau(
        monitor='val_loss',
        factor=0.5,
        patience=10,
        verbose=1
    )
]

deep_history = deep_model.fit(
    X_train, y_train,
    validation_data=(X_val, y_val),
    epochs=200,
    batch_size=32,
    callbacks=callbacks,
    verbose=1
)

print("\n✓ Deep network training completed!")
```

### 8.2: Compare Shallow vs Deep

```python
# Evaluate both models
shallow_loss, shallow_acc = model.evaluate(X_val, y_val, verbose=0)
deep_loss, deep_acc = deep_model.evaluate(X_val, y_val, verbose=0)

print("\n" + "="*70)
print("SHALLOW vs DEEP COMPARISON")
print("="*70)
print(f"\nShallow Network (2→10→1):")
print(f"  Parameters: {model.count_params():,}")
print(f"  Test Loss:  {shallow_loss:.4f}")
print(f"  Test Acc:   {shallow_acc:.2%}")

print(f"\nDeep Network (2→10→10→1):")
print(f"  Parameters: {deep_model.count_params():,}")
print(f"  Test Loss:  {deep_loss:.4f}")
print(f"  Test Acc:   {deep_acc:.2%}")

print(f"\nAccuracy Improvement: {(deep_acc - shallow_acc)*100:+.2f}%")
print("="*70)

# Plot training curves comparison
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.plot(history.history['loss'], label='Shallow - Train', linewidth=2)
plt.plot(deep_history.history['loss'], label='Deep - Train', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Training Loss Comparison')
plt.legend()
plt.grid(True, alpha=0.3)

plt.subplot(1, 3, 2)
plt.plot(history.history['val_loss'], label='Shallow - Val', linewidth=2)
plt.plot(deep_history.history['val_loss'], label='Deep - Val', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Validation Loss Comparison')
plt.legend()
plt.grid(True, alpha=0.3)

plt.subplot(1, 3, 3)
plt.plot(history.history['val_accuracy'], label='Shallow', linewidth=2)
plt.plot(deep_history.history['val_accuracy'], label='Deep', linewidth=2)
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.title('Validation Accuracy Comparison')
plt.legend()
plt.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```

### 8.3: Decision Boundary Comparison

```python
# decision boundaries side by side
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Shallow network
ax = plt.subplot(1, 2, 1)
x_min, x_max = X_val[:, 0].min() - 0.5, X_val[:, 0].max() + 0.5
y_min, y_max = X_val[:, 1].min() - 0.5, X_val[:, 1].max() + 0.5
xx, yy = np.meshgrid(np.linspace(x_min, x_max, 200),
                    np.linspace(y_min, y_max, 200))
mesh_input = np.c_[xx.ravel(), yy.ravel()]
Z_shallow = model.predict(mesh_input, verbose=0).reshape(xx.shape)

plt.contourf(xx, yy, Z_shallow, levels=20, cmap='RdYlBu', alpha=0.6)
plt.colorbar(label='Predicted Probability')
plt.scatter(X_val[y_val==0, 0], X_val[y_val==0, 1], 
           c='blue', label='Class 0', edgecolors='k', s=50)
plt.scatter(X_val[y_val==1, 0], X_val[y_val==1, 1], 
           c='red', label='Class 1', edgecolors='k', s=50)
plt.title(f'Shallow Network (Acc: {shallow_acc:.2%})')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.legend()

# Deep network
ax = plt.subplot(1, 2, 2)
Z_deep = deep_model.predict(mesh_input, verbose=0).reshape(xx.shape)

plt.contourf(xx, yy, Z_deep, levels=20, cmap='RdYlBu', alpha=0.6)
plt.colorbar(label='Predicted Probability')
plt.scatter(X_val[y_val==0, 0], X_val[y_val==0, 1], 
           c='blue', label='Class 0', edgecolors='k', s=50)
plt.scatter(X_val[y_val==1, 0], X_val[y_val==1, 1], 
           c='red', label='Class 1', edgecolors='k', s=50)
plt.title(f'Deep Network (Acc: {deep_acc:.2%})')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.legend()

plt.tight_layout()
plt.show()
```

---

## Submission

Save your completed notebook with all code cells executed:

1. All code cells with outputs
2. All visualizations

**File name:** `LastName_FirstName_NN_Assignment.ipynb`
