# Attribute Index Fix

Magento 2 supports custom source models for attributes except for indexing them into the `catalog_product_index_eav`
table (which feeds layered navigation).

The original problem is found in `\Magento\Catalog\Model\ResourceModel\Product\Indexer\Eav\Source:302` where it ensures
that the values saved exist in the `eav_attribute_option` table. When using that custom source model, those values do not
exist.

The first / easy solution is to comment out those lines. That doesn't work for production so a more durable
method needs to be had. While using a `preference` is not preferrable, this will solve the problem in the short term.

Here is how to get this running:

* `composer require-dev swiftotter/attribute-index-fix`
* `php bin/magento module:enable SwiftOtter_AttributeIndexFix`
* `php bin/magento cache:clean`