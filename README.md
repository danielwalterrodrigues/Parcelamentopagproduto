# Parcelamentopagproduto
Paracelamento na página de produdo para PagSeguro

O módulo nao está 100% operacional. É importante inserir o código abaixo no seu view.phtml

O código também nao está 100%, vou alterar e fazer um "for" para cada tipo de parcela. Mas funciona :-)

Contribuiçoes sao muito bem vindas

//////////////////////////////////////////////////////////////////////////////////////////////////////////

Inserir este código na página de produto (app/design/frontend/tema/tema/template/catalog/product/view.phtml

<!-- ////////////////// opcoes de parcelamento ////////////////////// -->
<?php
	
	$precoproduto = $product->getFinalPrice();
	$juros = Mage::getStoreConfig('parcelapagproduto/configuracoes/juros');
	$maxparcelas = Mage::getStoreConfig('parcelapagproduto/configuracoes/maxparcelas');
	$maxsemjuros = Mage::getStoreConfig('parcelapagproduto/configuracoes/maxsemjuros');
	$minvalor = Mage::getStoreConfig('parcelapagproduto/configuracoes/minvalor');
	$descboleto = Mage::getStoreConfig('parcelapagproduto/configuracoes/descboleto');

?>	

	<?php 
	$valormin = $precoproduto / 2;
	if ($minvalor <= $valormin && $maxparcelas >= 2) {
		echo "<div><b>Opç&otilde;es de parcelamento para este produto:</b></div>";
	} ?>

<div style="padding: 10px;">
	<?php 

	// parcela 2
	$valor2 = ($precoproduto / 2);
	if ($minvalor <= $valor2 && $maxparcelas >= 2) {
		echo "2x de R$".number_format($valor2, 2, ',', '.')." sem juros<br />";
	}
	

	// parcela 3
	$valor3 = ($precoproduto / 3);
	$precoprodutofinal3 = ($precoproduto * 34.33) / 100;
	if ($minvalor <= $valor3 && $maxparcelas >= 3) {
	if ($maxsemjuros < 3) {
		echo "3x de R$".number_format($precoprodutofinal3, 2, ',', '.')." com juros<br />";
	} else {
		echo "3x de R$".number_format($valor3, 2, ',', '.')." sem juros<br />";
	}
	}

	// parcela 4
	$valor4 = ($precoproduto / 4);
	$precoprodutofinal4 = ($precoproduto * 24.98) / 100;
	if ($minvalor <= $valor4 && $maxparcelas >= 4) {
	if ($maxsemjuros < 4) {
		echo "4x de R$".number_format($precoprodutofinal4, 2, ',', '.')." com juros<br />";
	} else {
		echo "4x de R$".number_format($valor4, 2, ',', '.')." sem juros<br />";
	}
	}

	// parcela 5
	$valor5 = ($precoproduto / 5);
	$precoprodutofinal5 = ($precoproduto * 20.58) / 100;
	if ($minvalor <= $valor5 && $maxparcelas >= 5) {
	if ($maxsemjuros < 5) {
		echo "5x de R$".number_format($precoprodutofinal5, 2, ',', '.')." com juros<br />";
	} else {
		echo "5x de R$".number_format($valor5, 2, ',', '.')." sem juros<br />";
	}
	}

	// parcela 6
	$valor6 = ($precoproduto / 6);
	$precoprodutofinal6 = ($precoproduto * 17.4) / 100;
	if ($minvalor <= $valor6 && $maxparcelas >= 6) {
	if ($maxsemjuros < 6) {
		echo "6x de R$".number_format($precoprodutofinal6, 2, ',', '.')." com juros<br />";
	} else {
		echo "6x de R$".number_format($valor6, 2, ',', '.')." sem juros<br />";
	}
	}
	$valorboleto = $precoproduto - (($precoproduto / 100) * $descboleto);
	if ($descboleto > 0) {
	echo "Apenas <b>R$".number_format($valorboleto, 2, ',', '.')."</b> com <b>".$descboleto."%</b> de desconto no boleto.";
	}
	

	// frase final
	if ($minvalor <= $valor2 && $maxparcelas >= 2) {
	echo "<p style='margin-top:5px;'>Todas as opç&ocirc;es você encontra no fechamento do pedido.</p>";
	}

	?>
</div>
<!-- ////////////////// opcoes de parcelamento ////////////////////// -->
