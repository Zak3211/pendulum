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
| `pendulum.py` | Double pendulum integrated with semi-implicit (symplectic) Euler and drawn live with `tkinter`. Includes an energy function for checking the integrator. |
| `double_pendulum.py` | Two double pendulums whose starting angles differ by 10⁻⁹ rad, run side by side with traces, to show sensitivity to initial conditions (chaos). |

### Machine learning basics: `neural_networks/`

| File | What it shows |
| --- | --- |
| `neuron.py`, `xor_network.py` | A step-activation neuron. AND, OR and NAND gates built by hand, then combined into XOR. |
| `gradient_descent.py` | Gradient descent on a 1-D function in a few lines. |
| `neural_net.py` | A minimal NumPy feed-forward network. |
| `mnist_classification.py` | A two-layer PyTorch MNIST classifier. Trains, tests and exports its weights to JSON. |
| `mnist_class.py` | Loads the exported weights into the NumPy network and evaluates it on the test set. |

### Genetic algorithms: pendulum control

| File | What it shows |
| --- | --- |
| `single_pendulum/single_pendulum.py` | Pendulum on a cart, driven by the cart's acceleration. |
| `single_pendulum/pendulum_net.py` | Small fixed-architecture network with mutation-only reproduction. |
| `single_pendulum/pendulum_sim.py` | Selection loop: mutate, score, keep the top 5. Also displays the best controller. |
| `NEAT Algorithm/double_pendulum.py` | Double pendulum on a cart. |
| `NEAT Algorithm/gnn.py` | NEAT-style graph network whose topology evolves: add or remove nodes and connections. |
| `NEAT Algorithm/neat_sim.py` | Evolution loop with separate fitness functions for swing-up and for balancing, plus a visualiser. |
| `neat_net.py` | An earlier layered prototype of the NEAT network. |

## Running

You need Python 3 with `numpy` and `matplotlib`. The MNIST scripts also need `torch` and `torchvision`. Visualisations use `tkinter`.

```bash
pip install numpy matplotlib torch torchvision
python pendulum.py
```

Scripts use relative paths, so run each one from inside its own folder. The MNIST dataset and the evolved populations (`*.pkl`) aren't committed:

- `mnist_classification.py` downloads MNIST and regenerates `MNIST_Classification.json`, the trained weights that `mnist_class.py` loads.
- The evolution scripts read and write their population pickles. Use `resetNetworks()` in `neat_sim.py` to start a fresh population.
