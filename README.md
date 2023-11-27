import numpy as np

class Matrix:

    def __init__(self, rows, cols):
        self.matrix = np.zeros((rows, cols))

    def input_matrix(self):
        for i in range(len(self.matrix)):
            row = input(f"Enter values for row {i + 1} (comma-separated): ")
            for x in range(len(self.matrix[0])):
                self.matrix[i][x] = float(row.split(",")[x])

    def display_matrix(self):
        print("/////\\\\\\\\\\\\\\\\\\\\", len(self.matrix[0]))
        for i in range(len(self.matrix)):
            print(self.matrix[i])

    def add(self, other_matrix):
        return Matrix(*self.matrix.shape)._apply_operation(self.matrix + other_matrix.matrix)

    def subtract(self, other_matrix):
        return Matrix(*self.matrix.shape)._apply_operation(self.matrix - other_matrix.matrix)

    def multiply(self, other_matrix):
        return Matrix(*np.dot(self.matrix, other_matrix.matrix).shape)._apply_operation(np.dot(self.matrix, other_matrix.matrix))

    def transpose(self):
        return Matrix(*self.matrix.T.shape)._apply_operation(self.matrix.T)

    def inverse(self):
        try:
            inv_matrix = np.linalg.inv(self.matrix)
            return Matrix(*inv_matrix.shape)._apply_operation(inv_matrix)
        except np.linalg.LinAlgError:
            print("Matrix is singular. Cannot find the inverse.")
            return None

    def solve_linear_system(self, b):
        try:
            solution = np.linalg.solve(self.matrix, b)
            return Matrix(*solution.shape)._apply_operation(solution)
        except np.linalg.LinAlgError:
            print("Matrix is singular or not square. Cannot solve the system.")
            return None

    def eigenvalues(self):
        eig_vals, _ = np.linalg.eig(self.matrix)
        return eig_vals

    def eigenvectors(self):
        _, eig_vecs = np.linalg.eig(self.matrix)
        return Matrix(*eig_vecs.shape)._apply_operation(eig_vecs)

    def norm(self):
        return np.linalg.norm(self.matrix)

    def _apply_operation(self, result_matrix):
        new_matrix = Matrix(*result_matrix.shape)
        new_matrix.matrix = result_matrix
        return new_matrix

    def __iter__(self):
        self._current_row = 0
        self._current_col = 0
        return self

    def __next__(self):
        if self._current_row < len(self.matrix):
            value = self.matrix[self._current_row, self._current_col]
            self._current_col += 1
            if self._current_col == len(self.matrix[0]):
                self._current_col = 0
                self._current_row += 1
            return value
        else:
            raise StopIteration

    def spiral_iterator(self):
        rows, cols = self.matrix.shape
        left, right, top, bottom = 0, cols - 1, 0, rows - 1

        while left <= right and top <= bottom:
            for i in range(left, right + 1):
                yield self.matrix[top, i]
            top += 1

            for i in range(top, bottom + 1):
                yield self.matrix[i, right]
            right -= 1

            if top <= bottom:
                for i in range(right, left - 1, -1):
                    yield self.matrix[bottom, i]
                bottom -= 1

            if left <= right:
                for i in range(bottom, top - 1, -1):
                    yield self.matrix[i, left]
                left += 1

- 👋 Hi, I’m @Neo961 journalist looking for the thruth
- 👀 I’m interested in music, books, culture, world.
- 🌱 I’m currently learning the begining of the world, how everithing works.
- 💞️ I’m looking to collaborate on how to save pur current world and to give freedom to slave people 
- 📫 How to reach me you can contact me on my email ndromero@rainbowonderlust.com
- ♾️ karma is a bitch, but i also can help karma to make is work
- Without fear to fight for the right things.
- 🌎 this world have to change, the rules of the game are not fair, people are goverments slaves.
- 🔖 just take a minutw to analize everything how and since when. 
- 🐉 drakaris
Neo961/Neo961 is a ✨ special ✨ repository because its `the creator, the mage, he got the key to open and close the paths` (wizard)
- ✡️ the stars are mor close than we thoght
- 👨🏻‍🎓 im the boss.
- 🌧️ i can make this possible 
- ♾️my energy is only mind and no one is allowed to take it.
- 👹🤯 my power is only mine and no one has control over this only me.
- 😎 no one is allow to see through my eyes only me.
- my power play with the time.
- nadie puede ver atraves de mi ojo.
- mi cerebro se mantiene libre de mal pensamiento.
- nadie puede esxuchar mis pensamientos
- la luna es una conmigo
  <Deus> cambio el tiempo y pidio mas timepo para cambiar las cosas.
**Matrix de personalidad para Neo**

**Nombre:** Neo

**Edad:** 27

**Sexo:** Masculino

**Ocupación:** Programador

**Personalidad:**

* Inteligente
* Creativo
* Rebelde
* Idealista
* Compasivo

**Valores:**

* La verdad
* La libertad
* La justicia
* La igualdad
* El amor

**Objetivos:**

* Liberar a la humanidad de la Matrix
* Proteger a los demás
* Hacer del mundo un lugar mejor

**Historia:**

Neo es un programador que vive en la ciudad de Matrix. Él es un hombre inteligente y creativo, pero también es rebelde e idealista. Un día, Neo conoce a Morfeo, un hombre que le dice que la Matrix no es real. Morfeo le enseña a Neo cómo usar sus poderes y le ayuda a liberarse de la Matrix.

**Dimensiones:**

La dimensión de Neo sería una realidad que refleja sus valores y objetivos. Sería un mundo donde la verdad, la libertad, la justicia, la igualdad y el amor son la norma. En esta dimensión, Neo sería un héroe que lucha por un mundo mejor.

**Detalles:**

Aquí hay algunos detalles específicos que podrías incluir en la dimensión de Neo:

* La tecnología sería avanzada y sostenible.
* La sociedad sería justa e igualitaria.
* El arte y la cultura serían abundantes y vibrantes.
* La naturaleza estaría protegida y conservada.

**Escenarios:**

Aquí hay algunos escenarios que podrían ocurrir en la dimensión de Neo:

* Neo podría luchar contra las máquinas para liberar a la humanidad.
* Podría ayudar a crear un nuevo mundo mejor para todos.
* Podría inspirar a otros a luchar por la verdad, la libertad y la justicia.

**Final:**

El final de la dimensión de Neo sería abierto. Podría terminar con Neo triunfando en su misión de liberar a la humanidad, o podría terminar con Neo enfrentándose a un nuevo desafío.
