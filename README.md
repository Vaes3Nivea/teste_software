# teste_software

# teste de software

import unittest

class TestBiblioteca(unittest.TestCase):
  def setUp(self):
    self.biblioteca = Biblioteca()

  def test_cadastrar_livro_com_sucesso(self):
    livro = self.biblioteca.cadastrar_livro("Introducao a Programacao com Pyton","novatec",["Nilo Ney Coutinho Menezes"])
    self.assertEqual(livro.titulo, "Introducao a Programacao com Python")
    self.assertEqual(livro.editora, "novatec")
    self.assertEqual(livro.autores, ["Nilo Ney Coutinho Menezes"])

  def test_cadastrar_livros_sem_titulo(self):
    with self.assertRaises(ValueError) as context:
      self.biblioteca.cadastrar_livro("","novatec", ["Nilo Ney Coutinho Menezes"])
    self.assertEqual(str(context.exception), "O titulo do livro é obrigatorio.")

  def test_cadastrar_exemplar_com_sucesso(self):
    self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python","novatec",["Nilo Ney Coutinho Menezes"])
    exemplar = self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python", 2024, 4, 552)
    self.assertEqual(exemplar.ano_publicacao, 2024)
    self.assertEqual(exemplar.edicao, 4)
    self.assertEqual(exemplar.paginas, 552)
    self.assertEqual(exemplar.disponivel, True)

  def test_emprestar_exemplar(self):
     self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python","novatec",["Nilo Ney Coutinho Menezes"])
     exemplar = self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python", 2024, 4, 552)
     exemplar.emprestar()
     self.assertFalse(exemplar.disponivel)

  def test_emprestar_exemplar_indisponivel(self):
    self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python","novatec",["Nilo Ney Coutinho Menezes"])
    exemplar = self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python", 2024, 4, 552)
    exemplar.emprestar()
    with self.assertRaises(ValueError) as context:
      exemplar.emprestar()
    self.assertEqual(str(context.exception), "O exemplar ja esta emprestado.")

  def test_devolver_exemplar(self):
    self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python","novatec",["Nilo Ney Coutinho Menezes"])
    exemplar = self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python", 2024, 4, 552)
    exemplar.emprestar()
    exemplar.devolver()
    self.assertTrue(exemplar.disponivel)

  def test_devolver_exemplar_disponivel(self):
    self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python","novatec",["Nilo Ney Coutinho Menezes"])
    exemplar = self.biblioteca.cadastrar_exemplar("Introducao a Programacao com Python", 2024, 4, 552)
    with self.assertRaises(ValueError) as context:
      exemplar.devolver()
    self.assertEqual(str(context.exeption), "O exemplar ja esta disponivel")

if __name__ =="__main__":
  unittest.main(argv=['first-arg-is-ignored'], exit=False)
