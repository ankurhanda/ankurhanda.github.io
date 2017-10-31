---
title: DDPG Explained
---

## DDPG

**Experience Replay**

```python
class ReplayBuffer(object):

    def __init__(self, buffer_size, random_seed=123):

        self.buffer_size = buffer_size
        self.count = 0
        self.buffer = []
        self.buffer_filled = False
        random.seed(random_seed)

    def add(self, s, a, r, t, s2):

        experience = (s, a, r, t, s2)

        if not self.buffer_filled:
            self.buffer.append(experience)
        else:
            self.buffer[self.count] = experience

        if self.count == self.buffer_size - 1 and not self.buffer_filled:
            self.buffer_filled = True

        self.count = (self.count + 1) % self.buffer_size

    def size(self):
        if not self.buffer_filled:
            return self.count
        else:
            return self.buffer_size-1

    def sample_batch(self, batch_size):

        batch = []

        if self.count < batch_size and self.buffer_filled==False:
            batch = random.sample(self.buffer, self.count)
        else:
            batch = random.sample(self.buffer, batch_size)

        s_batch = np.array([_[0] for _ in batch])
        a_batch  = np.array([_[1] for _ in batch])
        r_batch  = np.array([_[2] for _ in batch])
        t_batch  = np.array([_[3] for _ in batch])
        s2_batch = np.array([_[4] for _ in batch])

        return s_batch, a_batch, r_batch, t_batch, s2_batch

    def clear(self):
        self.buffer = []
        self.count = 0
```