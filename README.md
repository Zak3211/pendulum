# Pendulum Project

This is one of my first projects. I wrote it to run workshops that introduced first-year students to three topics:

- **Basic machine learning**: single neurons, small hand-built networks and an MNIST classifier
- **Numerical algorithms**: integrating the equations of motion of single and double pendulums
- **Genetic algorithms**: evolving controllers that swing up and balance a pendulum on a moving cart

The code is kept close to how it was used in the sessions: short scripts that each make one idea visible. It is not meant to be a polished library.

## Contents

### Numerical simulation: double pendulum

| File | What it shows |
| --- | --- |
| `Pendulum.py` | Double pendulum integrated with semi-implicit (symplectic) Euler and drawn live with `tkinter`. Includes an energy function for checking the integrator. |
| `2Pendulums.py` | Two double pendulums whose starting angles differ by 10⁻⁹ rad, run side by side with traces, to show sensitivity to initial conditions (chaos). |

### Machine learning basics: `Neural Networks/`

| File | What it shows |
| --- | --- |
| `Neuron.py`, `XORNetwork.py` | A step-activation neuron. AND, OR and NAND gates built by hand, then combined into XOR. |
| `gradient_descent.py` | Gradient descent on a 1-D function in a few lines. |
| `NeuralNet.py` | A minimal NumPy feed-forward network. |
| `MNIST_Classification.py` | A two-layer PyTorch MNIST classifier. Trains, tests and exports its weights to JSON. |
| `MNIST_Class.py` | Loads the exported weights into the NumPy network and evaluates it on the test set. |

### Genetic algorithms: pendulum control

| File | What it shows |
| --- | --- |
| `Single Pendulum/SinglePendulum.py` | Pendulum on a cart, driven by the cart's acceleration. |
| `Single Pendulum/pendulumNet.py` | Small fixed-architecture network with mutation-only reproduction. |
| `Single Pendulum/PendulumSimulation.py` | Selection loop: mutate, score, keep the top 5. Also displays the best controller. |
| `NEAT Algorithm/DoublePendulum.py` | Double pendulum on a cart. |
| `NEAT Algorithm/GNN.py` | NEAT-style graph network whose topology evolves: add or remove nodes and connections. |
| `NEAT Algorithm/NEATSim.py` | Evolution loop with separate fitness functions for swing-up and for balancing, plus a visualiser. |
| `NEAT_net.py` | An earlier layered prototype of the NEAT network. |

## Running

You need Python 3 with `numpy` and `matplotlib`. The MNIST scripts also need `torch` and `torchvision`. Visualisations use `tkinter`.

```bash
pip install numpy matplotlib torch torchvision
python Pendulum.py
```

Scripts use relative paths, so run each one from inside its own folder. Datasets and trained networks (`*.pkl`, the MNIST weights JSON) aren't committed:

- `MNIST_Classification.py` downloads MNIST and regenerates the weights.
- The evolution scripts read and write their population pickles. Use `resetNetworks()` in `NEATSim.py` to start a fresh population.
